<template>
    <div id="main-banner">
        <h1>Make Your Burger</h1>
    </div>
</template>

<script>
export default {
    name:"Banner"
}
</script>

<style scoped>
    #main-banner {
        background: url('/img/burger.jpg') center / cover;
        background-position: 0 -250px;
        /*background-size: cover;*/
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1 {
        color: #fff;
        text-align: center;
        background-color: #222;
        font-size: 3.5rem;
        padding: .5rem .8rem;
    }
</style>