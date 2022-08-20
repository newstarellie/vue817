<script>
export default {
  props: ['taskName', 'deleted', 'completed', 'id'],
  data() {
    return {
      itemId: this.id,
      itemDeleted: this.deleted,
      itemCompleted: this.completed,
    };
  },
  methods: {
    deletedItem: function () {
      this.itemDeleted = true;
      this.$emit('itemDeleted', this.itemId);
    },
  },
  watch: {
    itemCompleted: function () {
      let data = {
        id: this.itemId,
        completed: this.itemCompleted,
      };
      this.$emit('itemCompleted', data);
    },
  },
};
</script>

<template>
  <li v-if="!deleted" :class="{ completedClass: itemCompleted }">
    {{ taskName }}
    <button @click="deletedItem()">X</button>
    <input type="checkbox" v-model="itemCompleted" />
  </li>
</template>

<style scoped>
h2 {
  color: red;
  font-size: 1.2rem;
}
span {
  border: 1px solid black;
  padding: 0 5px;
  margin: 2px;
}
li {
  position: relative;
  width: 150px;
  list-style: none;
  padding: 10px;
}
li > input {
  position: absolute;
  left: -20px;
}
.completedClass {
  text-decoration: line-through;
  color: gray;
}
</style>
