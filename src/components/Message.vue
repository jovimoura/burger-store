<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name:'Message',
    props: {
        msg:String
    }
}
</script>

<style scoped>
    p {
        color:#004085;
        background-color: #cce5ff;
        border: 2px solid #b8daff;
        border-radius: 5px;
        margin: 1.2rem auto;
        max-width: 20rem;
        padding: .8rem;

    }
</style>