<template>
  <div>
    
    <Navbar :logo="logo_src" :alt="app_name" />

    <router-view/>

    <Footer />

  </div>

</template>

<script>
import Footer from './components/Footer.vue'
import Navbar from './components/Navbar.vue'
export default {
  components: { Navbar, Footer },

  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Monte seu Skate"
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
    margin: 15px;
    min-height: 300px;
  }

  h1 {
    text-align: center;
    font-size: 22px;
    margin-bottom: 10px;
    color: #1c1c1c;
  }

</style>
