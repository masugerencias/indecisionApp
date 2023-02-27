<template>
    <div>
        <img 
        :src="img" 
        alt="bg">
        <div class="bg-dark">
            <input type="text" placeholder="ask me a question" v-model="question">
            <p>Recuerda que tienes que poner un signo de interrogación (?) al final</p>
            <div>
                {{ question }}
                <!-- este hace ref a DATA, ojo! -->
               <h1>{{ answer === 'yes' ? 'Si' : 'No hombre no' }}</h1> 
            </div>
        </div>
    </div>
</template>
<script>

export default {
    data() {
        return {
            question: null,
            answer: null,
            img: null
        }
    },
    methods: {
        async getAnswer() {
            this.answer = 'Pensando'
            await fetch("https://yesno.wtf/api")
                .then((response) => response.json())
                .then((data) => {
                this.answer = data.answer;
                this.img = data.image;
                console.log(data)
                    });
        },
    },
    watch: {
        //enviar con interrogacion y no enter...
        question() {
            if (this.question.includes('?')) {
                this.getAnswer()
                //s hace falta poner parentesis.
            }
        },
    }

}
</script>
<style>

body{
    background-color: whitesmoke;

}

</style>