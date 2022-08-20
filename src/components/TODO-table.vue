<script>
import TODOInput from './TODO-input.vue';
import TODOTaskItem from './TODO-taskItem.vue';
export default {
  components: { TODOInput, TODOTaskItem },
  data() {
    return {
      allTaskArr: [],
      renderTaskArr: this.allTaskArr,
      status: 0,
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
      taskObj.id = this.allTaskArr.length + 1;
      this.allTaskArr.push(taskObj);
    },
    deleteAllTask: function () {
      this.allTaskArr = [];
    },
    completed(data) {
      let id = data.id;
      let completed = data.completed;
      for (let i = 0; i < this.allTaskArr.length; i++) {
        if (id == this.allTaskArr[i].id) {
          this.allTaskArr[i].completed = completed;
        }
      }
    },
    deleted(id) {
      console.log(id);
      for (let i = 0; i < this.allTaskArr.length; i++) {
        if (id == this.allTaskArr[i].id) {
          this.allTaskArr[i].deleted = true;
        }
      }
    },
    statusHandler: function () {
      console.log('123');
      switch (this.status) {
        case 1:
          this.renderTaskArr = this.allTaskArr;
          console.log(this.renderTaskArr);
          break;
        case 2: //進行 C : F D: F
          this.renderTaskArr = [];
          for (let i = 0; i < this.allTaskArr.length; i++) {
            if (
              false == this.allTaskArr[i].completed &&
              false == this.allTaskArr[i].deleted
            ) {
              this.renderTaskArr.push(this.allTaskArr[i]);
              console.log('78975');
            }
          }
          console.log(this.renderTaskArr);
      }
    },
  },
  watch: {
    status: 'statusHandler',
    allTaskArr: {
      handler(newValue, oldValue) {
        console.log(newValue == oldValue);
        this.renderTaskArr = this.allTaskArr;
      },
      deep: true,
    },
  },
};
</script>

<template>
  <div>
    <h2>TODO</h2>

    <h2>all: {{ allTaskArr }}</h2>
    <h2>renderTaskArr: {{ renderTaskArr }}</h2>
    <h2>{{ status }}</h2>
    <TODOInput @sendOut="getTask" @deleteAll="deleteAllTask" />
    <button @click="this.status = 1">全部</button>
    <button @click="this.status = 2">進行中</button>
    <button @click="this.status = 3">已完成</button>
    <button @click="this.status = 4">已刪除</button>
    <ul>
      <TODOTaskItem
        v-for="(item, index, key) in renderTaskArr"
        :taskName="item.taskName"
        :completed="item.completed"
        :deleted="item.deleted"
        :id="item.id"
        :index="index"
        :key="key"
        @itemCompleted="completed"
        @itemDeleted="deleted"
      />
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
