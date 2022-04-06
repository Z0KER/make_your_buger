<template>
    <div class="message-component">
        {{ msg }}
    </div>
</template>

<script>
export default {
    name: 'MessageComponent',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-component {
        color: #004085;
        background-color: #CCE5FF;
        border: 2px solid #B8DAFF;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
        text-align: center;
    }
</style>