<template>
    <button @click="goNext" >
        Next Step
    </button>
</template>

<script>
    export default {
        methods: {
            goNext() {
                this.$emit("goNext")
            }
        }
    }
</script>

<style scoped>
    button{
        position: absolute;
        bottom: 0;
        right: 0;
        cursor: pointer;
        color: white;
        padding: 14px 20px;
        border-radius: 10px;
        background-color: hsl(213, 96%, 18%);
        border: none;
        font-size: 14px;
        transition: 0.15s;
    }
    button:hover {
        background-color: hsl(213, 96%, 30%)
    }
</style>