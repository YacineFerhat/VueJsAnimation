<template>
    <div class="panel">
        <div class="panel-heading">
            <h3 class="title is-5 has-text-centered">
                {{question}}
            </h3>
        </div>

        <div class="panel-block">
            <div class="columns is-mobile">
                <div class="column is-one-third-desktop">
                    <button style="margin :10px" @click="onAnswer(btnData[0].correct)" class="btn btn-primary btn-lg">
                        {{btnData[0].answer}}
                    </button>
                </div>
                <div class="column is-one-third-desktop">
                    <button style="margin :10px" @click="onAnswer(btnData[1].correct)" class="btn btn-primary btn-lg">
                        {{btnData[1].answer}}
                    </button>
                </div>

                <div class="column is-one-third-desktop">
                    <button style="margin :10px" @click="onAnswer(btnData[2].correct)" class="btn btn-primary btn-lg">
                        {{btnData[2].answer}}
                    </button>
                </div>
                <div class="column is-one-third-desktop">
                    <button style="margin :10px" @click="onAnswer(btnData[3].correct)" class="btn btn-primary btn-lg">
                        {{btnData[3].answer}}
                    </button>
                </div>
            </div>
        </div>
    </div>
    

</template>


<script>
import { constants } from 'crypto';
    const MODE_ADDITION =1 ;
    const MODE_SUBSTRACTION = 2;

export default {
    data(){
        return{
            question : 'You have an error!',
            btnData : [
                {correct : true, answer : 0},
                {correct : false, answer : 0},
                {correct : false, answer : 0},
                {correct : false, answer : 0}
            ]
        };
    },
    methods:{
        generateQuestion(){
            const firstNumber = this.generateRandomNumber(1,100);
            const secondtNumber = this.generateRandomNumber(1,100);
            const modeNumber = this.generateRandomNumber(1,2);

            let correctAnswer = 0;

            switch(modeNumber){
                case MODE_ADDITION:
                    correctAnswer = firstNumber + secondtNumber;
                    //this.question = `What's  ${firstNumber}  +  ${secondNumber}  ?`;
                    this.question = 'What is ' + firstNumber + " + " + secondtNumber + ' ? ';
                    break;

                case MODE_SUBSTRACTION:
                    correctAnswer = firstNumber - secondtNumber;
                    //this.question = `What's ${firstNumber} - ${secondNumber}?`;
                    this.question = 'What is ' + firstNumber + '-' + secondtNumber + ' ? ';
                    break;
                
                default:
                    correctAnswer = 0;
                    this.question='Oops, an error occured ';
            }
            this.btnData[0].answer= this.generateRandomNumber(correctAnswer-10,correctAnswer+10,correctAnswer);
            this.btnData[0].correct=false;
            this.btnData[1].answer= this.generateRandomNumber(correctAnswer-10,correctAnswer+10,correctAnswer);
            this.btnData[1].correct=false;
            this.btnData[2].answer= this.generateRandomNumber(correctAnswer-10,correctAnswer+10,correctAnswer);
            this.btnData[2].correct=false;
            this.btnData[3].answer= this.generateRandomNumber(correctAnswer-10,correctAnswer+10,correctAnswer);
            this.btnData[3].correct=false;
            
            const correctButton = this.generateRandomNumber(0,3);
            
            this.btnData[correctButton].correct=true;
            this.btnData[correctButton].answer=correctAnswer;
        },

        generateRandomNumber(min,max,except){
            const rndNumber = Math.round(Math.random()*(max-min))+min;
            console.log(min,max,rndNumber);
            if(rndNumber== except){
                return this.generateRandomNumber(min,max,except);
            }
            return rndNumber;
        },

        onAnswer(isCorrect){
            this.$emit('answered',isCorrect);
        }
    },
    created(){
        this.generateQuestion();
    }
}
</script>


<style>

</style> 
