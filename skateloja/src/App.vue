<template>
  <div>
    
    <MenuPrincipal />

    <router-view/>

    <Footer />

  </div>

</template>

<script>
import Footer from './components/Footer.vue'
import MenuPrincipal from './components/MenuPrincipal.vue'
export default {
  components: { MenuPrincipal, Footer },
  
}
</script>

<style>

</style>
