<template>
  <div>
    <input type="text" v-model="content" />
    <button @click="addTodo">addTodo</button>
  </div>
</template>

<script>
export default {
  name: "TodoHeader",
  data() {
    return {
      content: "",
    };
  },
  methods: {
    // 添加todo
    addTodo() {
      this.$emit("addtodo", {
        id: new Date().getTime(),
        text: this.content,
        completed: false,
      });
      this.content = "";
    },
  },
};
</script>

<style scoped>
</style>