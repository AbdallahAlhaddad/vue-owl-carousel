<script>
import Vue from "vue";
import VueOwlCarousel from "@/xx-vue-owl-carousel.vue";

export default Vue.extend({
  name: "ServeDev",
  components: {
    XxVueOwlCarousel,
  },
});
</script>

<template>
  <div id="app">
    <xx-vue-owl-carousel />
  </div>
</template>
