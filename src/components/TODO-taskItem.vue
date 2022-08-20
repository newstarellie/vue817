<script>
export default {
  props: ['taskArrProp'],
  data() {
    return {
      taskArrPropOfItem: this.taskArrProp,
    };
  },
  methods: {
    deleteItem: function () {
      this.taskArrPropOfItem.deleted = true;
      console.log(this.taskArrPropOfItem);
      //我要把這個值傳出去 改變 外面的值
      //這邊只是改變視覺狀態
      //外面才能做分類
    },
    completedItem() {
      this.taskArrPropOfItem.completed = true;
    },
  },
};
</script>

<template>
  <li
    v-if="!this.taskArrPropOfItem.deleted"
    :class="{ completedClass: taskArrPropOfItem.completed }"
  >
    <input type="checkbox" @click="completedItem()" />
    {{ this.taskArrPropOfItem.name }}
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
