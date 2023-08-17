import { number } from 'yargs';
<template>
  <h2>{{name || 'Counter'}}</h2>
  <p>{{ counter }} <sup>2</sup> = {{getSquareValue()}} </p>
    <div>
      <button @click="increase" >+1</button>
      <button @click="decrease" >-1</button>
    </div>
</template>

<script>

export default {
    name:'Counter',
    props:{
        name: String,
        start: {
            type: Number,
            required: true,
            default:10,
        }
    },
    data(){
        return{
            counter: this.start
        }
    },
    methods:{
        getSquareValue(){
            return this.counter *  this.counter
        },
        increase(){
             this.counter++
        },
        decrease(){
             this.counter--
        }
    },
    computed:{
        squareCounter(){
            return this.counter + this.counter
        },
        customTitle(){
            return this.name == undefined ? 'Counter' : this.name
        }
    }   
}
</script>

<style>

    button{
        margin: 0 5px;
        background-color: #64BB87;
        color: white;
        cursor: pointer;
        border:'none';
        border-radius: 5px;
        padding: 5px 15px;
        transition: 0.3s ease-in-out;
    }
    button:hover{
        background-color: #5aa67b ;
        transition: 3.0s ease-in-out;
    }

</style>