<template>
  <div class="container_mouse_pointer">
    <img
      src="../assets/mouse_pointer.svg"
      alt="mouse_pointer"
      class="mouse_pointer"
      ref="mouse_pointer"
      @mousemove="handle_mousemove()"
    />
  </div>
</template>

<script>
export default {
  name: "mouse_pointer",

  props: {
    InformationMouse: {
      type: Object,
      required: true,
    },
  },

  mounted() {},

  methods: {
    updatePosition() {
      const mousePointer = document.querySelector(".mouse_pointer");
      mousePointer.style.left = `${this.InformationMouse.derectionX_mouse}px`;
      mousePointer.style.top = `${this.InformationMouse.derectionY_mouse}px`;
    },

    handle_mousemove() {
      const mousePointer = this.$refs.mousePointer;
      mousePointer.style.backgroundColor = "green";
      this.updatePosition();
    },
  },
};
</script>

<style scoped>
.mouse_pointer {
  width: 20px;
  height: 20px;
  background-color: red;
  /* border-radius: 50%; */
  position: absolute;
  pointer-events: none;
  /* transform: translate(-50%, -50%); */
}
</style>
