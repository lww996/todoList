<template>
  <div>
    <span class="span-btn" @click="filterTodo(0)" :class="{btnActive: filter === 0}">All</span>
    <span class="span-btn" @click="filterTodo(1)" :class="{btnActive: filter === 1}">Active</span>
    <span class="span-btn" @click="filterTodo(2)" :class="{btnActive: filter === 2}">Completed</span>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  data() {
    return {
      filter: 0,
    };
  },
  methods: {
    filterTodo(index) {
      this.filter = index;
      this.$emit("filtertodo", index);
    },
  },
};
</script>

<style scoped>
.span-btn {
  display: inline-block;
  padding: 3px 5px;
  cursor: pointer;
}

.btnActive {
  color: skyblue;
  font-size: 20px;
  border-bottom: 1px solid skyblue;
}
</style>