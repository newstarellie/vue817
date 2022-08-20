<script>
import TODOTaskItem from './TODO-taskItem.vue';
export default {
  data() {
    return {
      task: '',
    };
  },
  methods: {
    sendOutTask() {
      this.$emit('sendOut', this.task);
      this.task = '';
    },
    deleteAllTask() {
      this.$emit('deleteAllTask', '');
      console.log('完成');
    },
  },
  components: { TODOTaskItem },
  computed: {},
};
</script>

<template>
  <h2>{{ task }}</h2>
  <input
    type="text"
    placeholder="輸入要做的事情"
    v-model="task"
    v-on:keyup.enter="sendOutTask(this.task)"
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
