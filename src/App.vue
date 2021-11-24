<template>
  <Navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      logo_src: '/img/logo.png',
      app_name: 'Make your burger'
    }
  }
}
</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin:2rem;
    min-height: 15rem;
  }

  h1 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 1.2rem;
    color:#222;
  }

</style>
