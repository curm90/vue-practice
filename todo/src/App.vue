<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>
    <form @submit.prevent="addTodo()">
      <div class="form-group">
        <label for="exampleInputPassword1">New Todo</label>
        <input
          v-model="newTodo"
          type="text"
          class="form-control"
          aria-describedby="newTodoHelp"
          id="exampleInputPassword1"
          placeholder="Walk the dog..."
        />
        <small id="newTodoHelp" class="form-text text-muted">Enter a new todo</small>
      </div>
      <button type="submit" class="btn btn-primary">Add Todo</button>
    </form>
    <ul class="list-group mt-3">
      <li v-bind:key="todos[todo]" v-for="(todo, i) in todos" class="list-group-item">
        <button type="button" v-if="!todo.done" @click="markDone(todo)" class="btn btn-primary">Done</button>
        <button type="button" @click="removeTodo(i)" class="btn btn-danger">Delete</button>
        <span :class="{
            isDone: todo.done
          }">{{todo.title}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos = JSON.stringify(this.todos);
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos);
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false,
      });
      this.newTodo = "";
    },
    markDone(todo) {
      todo.done = true;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.isDone {
  text-decoration: line-through;
}
</style>
