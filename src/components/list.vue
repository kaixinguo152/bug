<template>
  <div class="container_list">
    <node v-for="node in bug" :key="node"></node>
  </div>
</template>

<script>
import { callWithErrorHandling } from "vue";
import node from "./node.vue";

//define the struct of node
class Node {
  //   constructor(derectionX, derectionY) {
  //     this.derectionX = derectionX;
  //     this.derectionY = derectionY;
  //     this.next = null;
  //   }
  constructor() {
    this.derectionX = 0;
    this.derectionY = 0;
    this.next = null;
  }
}

class List {
  constructor() {
    this.head = new Node();
    this.tail = this.head;
    this.length = 0;
  }

  AddNode(node) {
    console.log("added a node to " + this);

    if (!this.head) {
      this.head = new Node();
    }

    while (this.tail.next) {
      this.tail = this.tail.next;
    }
    this.tail.next = node;
    this.length++;
  }

  AddNode(number) {
    for (let i = 0; i < number; i++) {
      this.AddNode(new Node());
    }
  }

  UpdateList(InformationMouse) {
    const deltaX = InformationMouse.derectionX_mouse - this.head.derectionX;
    const deltaY = InformationMouse.derectionY_mouse - this.head.derectionY;
    const l = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
    const sin_sita = deltaY / l;
    const cos_sita = deltaX / l;

    let current = this.head;
    current.derectionX += cos_sita * 5;
    current.derectionY += sin_sita * 5;
    let current_ = current;
    current = current.next;
    while (current) {
      current.derectionX = current_.derectionX + cos_sita * 5;
      current.derectionY = current_.derectionY + sin_sita * 5;
      current_ = current_.next;
      current = current.next;
    }

    console.log("refreshed the list:" + this);
  }

  get_length() {
    let current = this.head;
    let count = 0;
    while (current) {
      count++;
      current = current.next;
    }
    this.length = count;
    return count;
  }
}

export default {
  name: "list",

  props: {
    InformationMouse: {
      type: Object,
      default: () => ({}),
    },
  },

  components: {
    node,
  },

  data() {
    return {
      bug: new List(),
    };
  },

  methods: {},
  mounted() {
    this.bug.AddNode(10);

    let current = this.bug.head;
    while (current) {
      current.style = {
        left: current.derectionX + "px",
        top: current.derectionY + "px",
      };
      current = current.next;
    }

    // setInterval(() => {
    //   this.bug.UpdateList(this.InformationMouse);
    // }, 500);
  },
};
</script>

<style scoped>
.container_list {
  width: 100vw;
  height: 100vh;
  background-color: black;
  border: 2px solid green;
}
</style>
