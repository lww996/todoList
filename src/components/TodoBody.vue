<template>
  <div>
    <transition-group name="move" tag="ul">
      <li v-for="(todo,index) in todolist" :key="todo.id" :class="{active:todo.completed}">
        <input type="checkbox" :checked="todo.completed" @change="$emit('togglestate',todo.id)" />

        <span v-show="showId != todo.id" @dblclick="dbl(todo.id,index)">{{todo.text}}</span>
        <input
          type="text"
          :value="todo.text"
          v-show="showId == todo.id"
          @blur="exit"
          @input="rewrite($event,todo.id)"
          ref="inp"
        />

        <button @click="removeTodo(todo.id)">删除</button>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "TodoBody",
  props: ["todolist"],
  methods: {
    // 删除todo
    removeTodo(id) {
      console.log(id);
      this.$emit("removetodo", id);
    },
    // 双击todo
    dbl(id, index) {
      this.showId = id;
      this.$nextTick(() => {
        this.$refs.inp[index].focus();
      });
    },
    // 重写todo
    rewrite(event, id) {
      this.$emit("rewritetodo", {
        content: event.target.value,
        id,
      });
    },
    // 修改todo后离开
    exit() {
      this.showId = "";
    },
  },
  data() {
    return {
      showId: "",
    };
  },
};
</script>

<style scoped>
ul {
  width: 605px;
}
li {
  width: 300px;
}
.active {
  text-decoration: line-through;
  color: #c0c0c0;
}
.move-enter,
.move-leave-to {
  opacity: 0;
  transform: translateX(100%);
}

.move-enter-active,
.move-leave-active {
  transition: all 0.3s linear;
}

.move-leave,
.move-enter-to {
  opacity: 1;
  transform: translateX(0);
}
</style>