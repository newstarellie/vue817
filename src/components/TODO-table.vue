<script>
import TODOInput from './TODO-input.vue';
import TODOTaskItem from './TODO-taskItem.vue';
export default {
  components: { TODOInput, TODOTaskItem },
  data() {
    return {
      taskArr: [],
    };
  },
  methods: {
    getTask: function (task) {
      this.taskArr.push(task);
    },
    deleteAllTask() {
      this.taskArr = [];
    },
  },
};
</script>

<template>
  <h2>TODO</h2>
  <h2>{{ taskArr }}</h2>
  <TODOInput @sendOut="getTask" @deleteAllTask="deleteAllTask" />
  <ul>
    <TODOTaskItem
      v-for="(item, index) in taskArr"
      :key="index"
      :taskName="item"
    >
    </TODOTaskItem>
  </ul>
</template>

<style scoped>
h2 {
  color: red;
  font-size: 1.2rem;
}
span {
  border: 1px solid black;
  margin: 2px;
}
</style>
