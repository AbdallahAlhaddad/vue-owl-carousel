<script>
import Vue from 'vue'
import VueOwlCarousel from '@/xx-vue-owl-carousel.vue'

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueOwlCarousel,
  },
})
</script>

<template>
  <div id="app">
    <vue-owl-carousel />
  </div>
</template>
