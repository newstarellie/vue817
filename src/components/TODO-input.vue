<script>
export default {
  data() {
    return {
      task: '',
    };
  },
  methods: {
    sendOutTask() {
      if (this.task) {
        this.$emit('sendOut', this.task);
        this.task = '';
      }
    },
    deletedAll() {
      this.$emit('deleteAll', this.task);
    },
  },
};
</script>

<template>
  <div>
    <h2>{{ task }}</h2>
    <input
      type="text"
      placeholder="輸入要做的事情"
      v-model="task"
      v-on:keyup.enter="sendOutTask()"
    />
    <button @click="sendOutTask()">送出</button>
    <button @click="deletedAll()">刪除全部</button>
  </div>
</template>

<style scoped>
h2 {
  color: red;
  font-size: 1.2rem;
}
</style>
