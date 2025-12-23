<template>
    <div class="node"" v-for="node in bug" :key="node">
        <node></node>
    </div>
</template>

<script>
import node from "./node.vue";
// import { defineProps } from "vue";

// const props = defineProps({
//     InformationMouse: {
//         type: Object,
//         default: () => ({ derectionX_mouse: 0, derectionY_mouse: 0 }),
//     }
// })

class Node {
    constructor(derectionX, derectionY) {
        this.derectionX = derectionX;
        this.derectionY = derectionY;
        this.next = null;
    }
}

class List {
    constructor() {
        this.head = new Node(null, null, null);
        this.length = 0;
    }

    AddNode(derectionX, derectionY) {
        console.log("added a node to " + this);

        if (!this.head) {
            this.head = new Node(null, null, null);
        }

        while (this.head.next) {
            this.head = this.head.next;
        }
        this.head.next = new Node(0, 0);
        this.length++;
    };

    RefreshList(myList) {
        console.log("refreshed the list:" + myList);
    };
}


export default {
    name: "list",

    props: {
        InformationMouse: {
            type: Object,
            default: () => ({}),
        }
    },

    components: {
        node,
    },

    data() {
        return {
            bug: new List(),
        }
    },

    methods: {
        // handleMouseMove() {
        //     this.clientX = e.clientX;
        //     this.clientY = e.clientY;
        // }
    },
    mounted() {
        // window.addEventListener("mousemove", this.handleMouseMove)
    },

    created() {
        for (var i = 0; i < 10; i++) {
            this.bug.AddNode(10, i * 10);
        }
    }
}
</script>

<style scoped>
.node {
    width: 10px;
    height: 10px;
    background-color: white;
}
</style>