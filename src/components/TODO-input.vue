<script>
export default {
  data() {
    return {
      task: '',
      taskToObj: {
        name: '',
        completed: false,
        deleted: false,
      },
    };
  },
  methods: {
    sendOutTask() {
      this.taskToObj.name = this.task;
      this.$emit('sendOut', this.taskToObj);
      this.task = '';
    },
    deleteAllTask() {
      this.$emit('deleteAllTask', '');
      console.log('完成');
    },
  },
  computed: {},
};
</script>

<template>
  <h2>{{ task }}</h2>
  <input
    type="text"
    placeholder="輸入要做的事情"
    v-model="task"
    v-on:keyup.enter="sendOutTask()"
  />
  <span v-on:click="sendOutTask(this.task)">送出</span>
  <span @click="deleteAllTask()">刪除全部</span>
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
