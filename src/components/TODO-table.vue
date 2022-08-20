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
      let taskObj = {
        id: '',
        taskName: '',
        completed: false,
        deleted: false,
      };
      taskObj.taskName = task;
      taskObj.id = this.taskArr.length + 1;
      this.taskArr.push(taskObj);
    },
    deleteAllTask: function () {
      this.taskArr = [];
    },
    completed(data) {
      let id = data.id;
      let completed = data.completed;
      for (let i = 0; i < this.taskArr.length; i++) {
        if (id == this.taskArr[i].id) {
          this.taskArr[i].completed = completed;
        }
      }
    },
    deleted(id) {
      console.log(id);
      for (let i = 0; i < this.taskArr.length; i++) {
        if (id == this.taskArr[i].id) {
          this.taskArr[i].deleted = true;
        }
      }
    },
  },
};
</script>

<template>
  <div>
    <h2>TODO</h2>
    <h2>{{ taskArr }}</h2>
    <TODOInput @sendOut="getTask" @deleteAll="deleteAllTask" />
    <ul>
      <TODOTaskItem
        v-for="(item, index, key) in taskArr"
        :taskName="item.taskName"
        :completed="item.completed"
        :deleted="item.deleted"
        :id="item.id"
        :index="index"
        :key="key"
        @itemCompleted="completed"
        @itemDeleted="deleted"
      >
        <div>123</div>
      </TODOTaskItem>
    </ul>
  </div>
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
