<template>
  <div class="container">

  </div>
</template>

<script>
import list from './components/list.vue';
export default {
  components: {
    list,
  },
  data() {
    return {
      derectionX_mouse,
      derectionY_mouse,
    }
  },

  mounted() {
    window.addEventListener("mousemove", this.handleMouseMove);
  },

  methods: {
    handleMouseMove(e) {
      this.derectionX_mouse = e.clientX;
      this.derectionY_mouse = e.clientY;
    }
  },
}

</script>

<style scoped>
.container {
  width: 100vw;
  height: 100vh;
  background-color: black;
}
</style>
