<template>
  <div id="app">
    <header>
      <h1>Todo App</h1>
    </header>
    <md-content class="md-elevation-5">
      <main>
        <md-field style="margin: 5px 15px; width: auto">
          <md-input
            placeholder="Type your todo"
            v-model="currentTodo"
            @keypress.enter="addtodo"
          ></md-input>
        </md-field>
        <TodoItem :todos="todos" v-on:del-todo="deleteTodo" />
      </main>
    </md-content>
    <!-- <HelloWorld msg="Welcome to Your Fue.js App"/> -->
  </div>
</template>

<script>
import TodoItem from "./components/TodoItem.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "App",
  components: {
    TodoItem,
  },
  data() {
    return {
      todos: [
        { title: "Go to bath", completed: false, id: uuidv4() },
        { title: "Make a game", completed: true, id: uuidv4() },
        { title: "Go to sleep", completed: false, id: uuidv4() },
      ],
      currentTodo: "",
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
    this.$watch(
      "todos",
      function() {
        console.log("Local storage updated");
        this.saveToLocal();
      },
      { deep: true }
    );
  },
  methods: {
    saveToLocal() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem("todos", parsed);
    },
    addtodo() {
      if (this.currentTodo.trim() === "") {
        return false;
      }
      this.todos.unshift({
        title: this.currentTodo,
        completed: false,
        id: uuidv4(),
      });

      this.currentTodo = "";
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);

    },
  },
};
</script>

<style>
@import url(./style.css);
</style>
