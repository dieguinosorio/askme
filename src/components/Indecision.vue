<template>
    <img v-if="urlImg" :src="urlImg" alt="bg"/>
    <div class="bg-dark"></div>
    <div class="indecision-container">
        <input type="text" v-model="question"  placeholder="Hazme una pregunta ?">
        <p>Recuerda terminar con un signo de interrogación (?)</p>
        <div v-if="isValidQuestion">
            <h2 v-text="question"></h2>
            <h1 v-text="answer"></h1>
        </div>

    </div>
</template>
<script>
const URL_ENDPOINT = 'https://yesno.wtf/api';
export default {
    data() {
        return {
            urlImg:null,
            question:null,
            answer:null,
            isValidQuestion:false
        }
    },

    watch:{
        question(newVal){
            this.isValidQuestion = false
            if(!newVal.includes('?')) return
            this.getAnswer();
            this.isValidQuestion = true
        }
    },

    methods: {
        async  getAnswer(url = URL_ENDPOINT, data = {}) {
            this.answer ="Pensando ...";
            const {answer,image} = await fetch(url).then(res=>{ return res.json()});
            this.answer = answer === 'yes' ? 'SI':'NO';
            this.urlImg = image;
        }
    },
}
</script>
<style scoped>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color:rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>