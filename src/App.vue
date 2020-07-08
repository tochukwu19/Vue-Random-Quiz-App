<template>
    <div>
        <h3>Random addition quiz</h3>
        <component :is="selected" :state="state"></component>
    </div>
</template>

<script>

import question from "./components/question";
import { eBus } from "./main"
import response from "./components/response"

export default {
    components: {
        question,
        response
    },                                         
    data(){            
        return{
            state: false,
            selected: "question"
        }
    },
    created(){
        // Listening to the emitted event and getting the data
        eBus.$on("answerClicked", (data) => {
            
            this.state = data;
            
            this.selected = "response";
        })

        eBus.$on("nextQuestion", (data) => {
            this.selected = "question"
        })
    }
}
</script>

<style scoped>
    h3{
        color: #fff;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-weight: lighter;
        text-align: center;
    }
</style>