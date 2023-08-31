<template>
    <button @click="goBack">
        Go Back
    </button>
</template>

<script>
    export default {
        methods:{
            goBack() {
                this.$emit("goBack")
            }
        }
    }
</script>

<style scoped>
    button{
        position: absolute;
        bottom: 0;
        left: 0;
        cursor: pointer;
        color: hsl(231, 11%, 63%);
        border: none;
        
        padding: 7px 0px;
        font-size: 16px;
        transition: 0.15s;
        font-weight: 500;
        background: none
    }
    button:hover {
        color: hsl(213, 96%, 18%);
        /* font-weight: 700; */
    }
</style>