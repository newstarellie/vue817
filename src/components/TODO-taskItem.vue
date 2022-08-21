<script>
export default {
  props: ['taskName', 'deleted', 'completed', 'id'],
  data() {
    return {
      itemId: this.id,
      itemDeleted: this.deleted,
      itemCompleted: this.completed,
      checkID: false,
    };
  },
  methods: {
    deletedItem: function () {
      this.itemDeleted = true;
      this.$emit('itemDeleted', this.itemId);
    },
    completedItem: function () {
      this.itemCompleted = true;
      this.$emit('itemCompleted', this.itemId);
    },
  },
  watch: {
    itemCompleted: function () {
      let data = {
        id: this.itemId,
        completed: this.itemCompleted,
      };
      this.$emit('itemCompleted', data);
      console.log(data);
    },
  },
  created() {
    console.log('重新渲染');
    if (this.itemId == this.id) {
      this.checkID = true;
    }
  },
  beforeUpdate() {
    console.log('更變化面');
    this.checkID = false;
    this.itemId = this.id;
    this.itemDeleted = this.deleted;
    this.itemCompleted = this.completed;
    if (this.itemId == this.id) {
      this.checkID = true;
    }
  },
};
</script>

<template>
  <li v-show="this.checkID" :class="{ completedClass: this.completed }">
    {{ taskName }}
    <button @click="deletedItem()">X</button>
    <button @click="completedItem()">完成</button>
    <span v-if="this.deleted">已刪除</span>
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
  background-color: red;
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
