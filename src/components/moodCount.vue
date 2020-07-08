<template>
    <h1>{{hello}}</h1>
</template>

<script>
import {eBus} from "../main"
export default {
    props: ["del"],
    data(){
        return{
            hello: ""
        }
    },
    // created(){
    //     eBus.$on("taskAdded", (data) => {
    //         this.hello = data
    //     })
    // }
}
</script>

<style scoped>

</style>