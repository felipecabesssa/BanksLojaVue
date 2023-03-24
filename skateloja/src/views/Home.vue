<template>
  <Banner />
  <div class="main-container">
    <h1>Monte seu Skate</h1>
    
    <SkateForm />

  </div>
</template>

<script>
import Banner from '@/components/Banner.vue'
import SkateForm from '@/components/SkateForm.vue'
export default {
  components: { Banner, SkateForm },
  
}
</script>