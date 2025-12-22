<template>
    <div class="node"" v-for="node in bug" :key="node">
        <node></node>
    </div>
</template>

<script>
import node from "./node.vue";
class Node {
    constructor(derectionX, derectionY) {
        this.derectionX = derectionX;
        this.derectionY = derectionY;
        this.next = null;
    }
}

class List {
    constructor() {
        this.head = null;
        this.length = 0;
    }

    AddNode(derectionX, derectionY) {
        console.log("added a node to " + this);


        if (!this.head) {
            head = new Node(null, null, null);
        }

        newnode = new Node(derectionX, derectionY);
        while (this.head.next != null) {
            this.head = List.head.next;
        }
        this.head.next = newnode;
        this.length++;
    };

    RefreshList(myList) {
        console.log("refreshed the list:" + myList);

    }
}


export default {
    name: "list",

    components: {
        node,
    },
    data() {
        return {
            bug: new List(),
        }
    },

    methods: {

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