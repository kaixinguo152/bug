<template>
  <div class="container">
    <node v-for="node in bug" :key="node"></node>
  </div>
</template>

<script>
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
    for (let i = 0; i < 10; i++) {
      this.bug.AddNode(new Node());
    }

    setInterval(() => {
      this.bug.UpdateList(this.InformationMouse);
    }, 500);
  },
};
</script>

<style scoped>
.container {
  width: 100vw;
  height: 100vh;
  background-color: green;
  border: 5px solid red;
}
</style>
