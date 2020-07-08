<template>
    <div class="question">
        <p>What is {{testData[0].question1}} + {{testData[0].question2}}?</p>
         <div class="options">
            <a v-for="(answer,i) in answers" :key="i" @click="checkAns(answer)">{{answer}}</a>
        </div>
    </div>
</template>

<script>
import { eBus } from "../main"
export default {
    data(){
        return {
            answers: [],
            correct: false,
            testData : [
                {
                    question1: "",
                    question2: ""
                },
                {
                    correctAnswer: ""
                },
                {
                    answerRange: [10,20]
                }
            ]
        }
    },
    methods:{

        // Checking if the answer is correct or false and passing that data to the parent component with the event bus
        checkAns(answer){
            if(answer === this.testData[1].correctAnswer){
                this.correct = true;
            }else{
                this.correct = false;
            }

            console.log(this.correct)

            eBus.$emit("answerClicked", this.correct)
        }
    },
    created(){
        // Creating random questions
        var q1 =  Math.floor(Math.random() * (10 - 1)) + 1
        var q2 =  Math.floor(Math.random() * (10 - 1)) + 1

        // Setting the questions for render
        this.testData[0].question1 = q1;
        this.testData[0].question2 = q2;

        // the answer for those questions
        var ans = q1 + q2;

        // setting the answer for render
        this.testData[1].correctAnswer = ans

        // Generating random incorrect answers 
        const arrL = 3;
        for(let i=0;i<arrL;i++){
            this.answers.push(Math.floor(Math.random()*(this.testData[2].answerRange[1] - this.testData[2].answerRange[0])) + this.testData[2].answerRange[0])
        }

        this.answers.push(this.testData[1].correctAnswer)

        function shuffle(array) {
            array.sort(() => Math.random() - 0.5);
        }

        shuffle(this.answers)
    }
}
</script>

<style scoped>
    .question{
        height: auto;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;        border-radius: 15px;
        background-color: rgb(63, 143, 209);
        -webkit-box-shadow: 2px 2px 2px 2px rgba(0,0,0,0.35);
        -moz-box-shadow: 2px 2px 2px 2px rgba(0,0,0,0.35);
        box-shadow: 2px 2px 2px 2px rgba(0,0,0,0.35);
        color: #fff;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-size: 22.5px;
    }
    .options{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
    }
    .options a{
        margin: 20px;
        width: 25px;
        text-align: center;
        padding: 10px;
        border-radius: 5px;
        background: rgb(20, 90, 122);
        color: #fff;
        cursor: pointer;
    }
</style>