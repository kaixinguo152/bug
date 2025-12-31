<template>
  <div class="mouse_pointer"></div>
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

  mounted() {
    // setInterval(() => {
    //   this.updatePosition();
    // }, 5);
    window.addEventListener("mousemove", this.updatePosition);
  },

  methods: {
    updatePosition() {
      const mousePointer = document.querySelector(".mouse_pointer");
      mousePointer.style.left = `${this.InformationMouse.derectionX_mouse}px`;
      mousePointer.style.top = `${this.InformationMouse.derectionY_mouse}px`;
    },
  },
};
</script>

<style scoped>
.mouse_pointer {
  width: 10px;
  height: 10px;
  background-color: white;
  border-radius: 50%;
  position: absolute;
  pointer-events: none;
  transform: translate(-50%, -50%);
}
</style>
