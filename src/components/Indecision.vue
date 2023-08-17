<template>
    <img :src="image" alt="bg">
    <div class="bg-dark">

    </div>
    <div class="indecision-container">
        <p>Ingrese una pregunta</p>
        <input type="text" placeholder="Hazme una pregunta" v-model="question">
        <p style="margin-top: 20px;">Recuerda terminar con un signo de interrogación (?)</p>
        
        <div v-show="isValidCuestion">
            <h2>{{question}}</h2>
            <h1>{{answer === 'yes' ? 'Si': 'No!' }}</h1>
        </div>

    </div>
</template>

<script>
export default {
    data(){
        return{
            question: '',
            answer: null,
            image: "",
            isValidCuestion: false
        }
    },
    methods:{
        async getAnswere(){
            this.answer = 'Pensando'
            const {answer,image} = await fetch('https://yesno.wtf/api').then(resp => resp.json())
            this.answer = answer
            this.image = image
        }
    },  
    watch:{
        question(value,oldValue){
            this.isValidCuestion = false
            if (!value.includes('?')) return
            this.isValidCuestion = true
            this.getAnswere()
        }
    }

}
</script>

<style>
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
        background-color: rgba(0, 0, 0, 0.4);
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