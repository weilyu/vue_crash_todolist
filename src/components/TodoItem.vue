<template>
  <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed" />
      {{todo.title}}
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      axios
        .put(`https://jsonplaceholder.typicode.com/todos/${this.todo.id}`, {
          completed: !this.todo.completed
        })
        .then(res => (this.todo.completed = res.data.completed))
        .catch(err => console.log(err));
    }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>