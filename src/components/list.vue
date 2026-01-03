<template>
  <div class="container_list" ref="container_list">
    <node v-for="node in bug.to_array()" :key="node"> </node>
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

  get_tail() {
    while (!this.head) {
      this.head = new Node();
    }

    const tail = this.head;
    while (tail.next) {
      tail = tail.next;
    }

    return tail;
  }

  AddNode(number) {
    let tail = this.get_tail();

    while (number-- > 0) {
      const newNode = new Node();
      tail.next = newNode;
      this.tail = newNode;
      console.log("added a node to " + this);

      tail = tail.next;
    }

    this.length += number;
  }

  // UpdateNode(node) {
  //   const deltaX = InformationMouse.derectionX_mouse - this.head.derectionX;
  //   const deltaY = InformationMouse.derectionY_mouse - this.head.derectionY;
  //   const l = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
  //   const sin_sita = deltaY / l;
  //   const cos_sita = deltaX / l;

  //   node.derectionX += cos_sita * 5;
  //   node.derectionY += sin_sita * 5;
  // }

  // UpdateList(InformationMouse) {
  //   const deltaX = InformationMouse.derectionX_mouse - this.head.derectionX;
  //   const deltaY = InformationMouse.derectionY_mouse - this.head.derectionY;
  //   const l = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
  //   const sin_sita = deltaY / l;
  //   const cos_sita = deltaX / l;

  //   let current = this.head;
  //   current.derectionX += cos_sita * 5;
  //   current.derectionY += sin_sita * 5;
  //   let current_ = current;
  //   current = current.next;
  //   while (current) {
  //     current.derectionX = current_.derectionX + cos_sita * 5;
  //     current.derectionY = current_.derectionY + sin_sita * 5;
  //     current_ = current_.next;
  //     current = current.next;
  //   }

  //   console.log("refreshed the list:" + this);
  // }
  update_list(derectionX_mouse, derectionY_mouse) {
    const list = document.querySelector(".container_list");

    for (let i = list.children.length - 1; i > 0; i--) {
      const current_node = list.children[i];
      const forhead_node = list.children[i - 1];
      //update the position of node
      current_node.style.left = forhead_node.style.left;
      current_node.style.top = forhead_node.style.top;
    }
    list.children[0].style.left = derectionX_mouse + "px";
    list.children[0].style.top = derectionY_mouse + "px";
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

  to_array() {
    const arr = [];
    let current = this.head;
    while (current) {
      arr.push(current);
      current = current.next;
    }
    return arr;
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

  computed: {
    link_list_to_array() {
      const arr = [];
      let current = this.bug.head;
      while (current) {
        arr.push(current);
        current = current.next;
      }
      return arr;
    },
  },

  mounted() {
    // this.bug.AddNode(10);

    // let current = this.bug.head;
    // while (current) {
    //   current.style = {
    //     left: current.derectionX + "px",
    //     top: current.derectionY + "px",
    //   };
    //   current = current.next;
    // }

    // const list = this.$refs.container_list;
    // console.log(list.children[1]);

    this.bug.AddNode(20);

    // window.addEventListener(
    //   "mousemove",
    //   this.bug.update_list(
    //     this.InformationMouse.derectionX_mouse,
    //     this.InformationMouse.derectionY_mouse
    //   )
    // );

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
