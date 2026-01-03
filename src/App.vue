<template>
  <div class="container">
    <list :InformationMouse="InformationMouse"></list>
    <mouse_pointer :InformationMouse="InformationMouse"></mouse_pointer>
  </div>
</template>

<script>
import list from "./components/list.vue";
import mouse_pointer from "./components/mouse_pointer.vue";

export default {
  components: {
    list,
    mouse_pointer,
  },

  data() {
    return {
      InformationMouse: {
        derectionX_mouse: 0,
        derectionY_mouse: 0,
      },
    };
  },

  mounted() {
    window.addEventListener("mousemove", (e) => {
      this.handleMouseMove(e);
      console.log(
        this.InformationMouse.derectionX_mouse,
        this.InformationMouse.derectionY_mouse
      );
    });
  },

  methods: {
    handleMouseMove(e) {
      this.InformationMouse.derectionX_mouse = e.clientX;
      this.InformationMouse.derectionY_mouse = e.clientY;
    },
  },
};
</script>

<style scoped>
.container {
  width: 100vw;
  height: 100vh;
  background-color: black;
  padding: 10px;
  border: 2px solid red;
}
</style>
