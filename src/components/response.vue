<template>
   <div :class="[!state ? 'danger' : '']">
      <p v-if=state>Subarashi! You got that right</p>
      <p v-else>Gomenasai! You'll get the next one</p>

      <button @click="next" :class="[!state ? 'dangerCol' : '']">Next Question</button>
   </div>
</template>

<script>

import {eBus} from "../main"
export default {
    props: ["state"],
    methods: {
       next(){
          eBus.$emit("nextQuestion", true)
       }
    }
}
</script>

<style scoped>
   div{
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      height: 200px;
      text-align: center;
      background-color: rgb(63, 143, 209);
      border-radius: 15px;
      padding: 20px;
      color: #fff;
      font-size: 21.5px;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
   }
   .danger{
      background-color: rgb(189, 92, 92);
   }
   .dangerCol{
         color: salmon;
   }
   button{
      padding: 10px;
      border: none;
      border-radius: 10px;
      font-size: 18px;
      color: royalblue;
      cursor: pointer;
   }
</style>