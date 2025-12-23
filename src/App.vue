<template>
  <div class="container">
    <list :InformationMouse="InformationMouse"></list>
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
      InformationMouse: {
        derectionX_mouse: 0,
        derectionY_mouse: 0,
      }
    }
  },

  mounted() {
    window.addEventListener("mousemove", this.handleMouseMove);
  },

  methods: {
    handleMouseMove(e) {
      setInterval(() => {
        console.log(e.clientX, e.clientY);
      }, 50);

      this.information_mouse.derectionX_mouse = e.clientX;
      this.information_mouse.derectionY_mouse = e.clientY;
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
