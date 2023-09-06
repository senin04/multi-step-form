<template>
    <button  @click="goNext">
        Confirm
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
        width: 103px;
        position: absolute;
        bottom: 0;
        right: 0;
        cursor: pointer;
        color: white;
        padding: 14px 20px;
        border-radius: 10px;
        background-color: hsl(243, 100%, 62%);
        border: none;
        font-size: 14px;
        transition: 0.15s;
    }
    button:hover {
        background-color: hsl(243, 100%, 72%);
    }
</style>