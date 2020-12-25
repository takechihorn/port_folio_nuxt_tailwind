<template>
  <div class=" bg-blue-200 h-screen w-screen">
    <div class=" md:justify-end">
      <Nav/>
    </div>
    <div>
      <Nuxt />
    </div>
    <div>
      <Footer/>
    </div>
  </div>
</template>


<script>
import Nav from '@/components/Nav.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios'

export default {
  components:{
    Nav,
    Footer
  }
}
</script>
<style>

</style>
