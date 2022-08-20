<script>
export default {
  props: ['taskArrProp'],
  data() {
    return {
      taskArrPropOfItem: this.taskArrProp,
      taskName: this.taskArrProp.name,
      taskDeleted: this.taskArrProp.deleted,
      taskCompleted: this.taskArrProp.completed,
    };
  },
  methods: {
    deleteItem: function () {
      this.taskDeleted = true;
    },
    completedItem() {
      this.taskCompleted = true;
    },
  },
};
</script>

<template>
  <li v-if="!taskDeleted" :class="{ completedClass: taskCompleted }">
    <input type="checkbox" @click="completedItem()" />
    {{ taskName }}
    <span @click="deleteItem()">X</span>
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
}
li > span {
  position: absolute;
  right: 0;
}
.completedClass {
  text-decoration: line-through;
  color: gray;
}
</style>
