<template>
  <div id="app">
    <TodoHeader @addtodo="addTodo"></TodoHeader>
    <TodoBody
      @removetodo="removeTodo"
      @togglestate="toggleState"
      @rewritetodo="rewriteTodo"
      :todolist="todosLists"
    ></TodoBody>
    <TodoFooter @filtertodo="filterTodo"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoBody from "./components/TodoBody";
import TodoFooter from "./components/TodoFooter";

// 假设远程仓库更新了
// let data = { name: "amy" }

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoBody,
    TodoFooter,
  },
  data() {
    return {
      todos: [
        { id: 1, text: "学习vue", completed: false },
        { id: 2, text: "学习webpack", completed: true },
        { id: 3, text: "学习ES6", completed: false },
      ],
      todoIndex: 0,
      ALL: 0,
      ACTIVE: 1,
      COMPLETED: 2,
    };
  },
  computed: {
    todosLists: function () {
      switch (this.todoIndex) {
        case this.ALL:
          return this.todos;
        case this.ACTIVE:
          return this.todos.filter((item) => item.completed != true);
        case this.COMPLETED:
          return this.todos.filter((item) => item.completed == true);
      }
      return this.todos;
    },
  },
  methods: {
    addTodo(options) {
      this.todos.push(options);
    },
    removeTodo(id) {
      this.todos = this.todos.filter((item) => {
        if (item.id !== id) {
          return item;
        }
      });
    },
    toggleState(id) {
      this.todos = this.todos.map((item) => {
        if (item.id == id) {
          item.completed = !item.completed;
          return item;
        }
        return item;
      });
    },
    rewriteTodo(obj) {
      this.todos = this.todos.map((item) => {
        if (item.id == obj.id) {
          item.text = obj.content;
          return item;
        }
        return item;
      });
    },
    filterTodo(index) {
      this.todoIndex = index;
    },
  },
};
</script>

<style>
</style>
