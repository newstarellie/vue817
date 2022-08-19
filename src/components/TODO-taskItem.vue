<script>
export default {
  props: ['taskName'],
  data() {
    return {
      message: 1,
      deleted: false,
    };
  },
  methods: {
    deleteItem: function () {
      this.deleted = true;
    },
  },
  computed: {},
};
</script>

<template>
  <li v-if="!deleted">
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
</style>
