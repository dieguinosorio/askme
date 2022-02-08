<template>
    <div>
        <h2>{{customTitle}}</h2>
        <p>{{counter}} <sup>2</sup> = {{squaredCounter}}</p>
        <div>
            <button @click.prevent="increase">+1</button>
            <button @click.prevent="decrease">-1</button>
        </div>
    </div>
</template>
<script>
export default {
    name:'Counter',
    props:{
        title:String,
        start:{
            type:Number,
            default:100,
            required:true,
            validator(value){
                return value >=0
            }
        }
    },
    data() {
        return {
            counter:this.start
        }
    },
    computed:{
        squaredCounter(){
            return this.counter * this.counter;
        },
        customTitle(){
            return this.title || 'Counter !!!'
        }
    },
    methods:{
        increase(){
            this.counter++;
        },
        decrease(){
            this.counter--;
        },
    }
}
</script>
<style>
button{
    background-color: #64B687;
    border-radius: 5px;
    border: 1px solid white;
    color: white;
    cursor: pointer;
    margin: 0 5px;
    padding: 5px 15px;
    transition: 0.3s ease-in-out;
}
button:hover {
    background-color: #5aa67b;
    transition: 0.3s ease-in-out;
}
</style>