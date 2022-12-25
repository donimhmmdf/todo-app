<template>
  <div class="container pt-4">
    <h2 class="text-lg font-bold mb-4">Todo Application</h2>
    <div class="flex w-full">
      <input
        @keyup.enter="addTodo"
        v-model="todo"
        type="text"
        class="p-2 w-full rounded-md mr-1 border border-gray-300 bg-gray-50"
      />
      <button
        @click="addTodo"
        class="py-2 px-3 bg-green-500 rounded-md text-white font-medium"
      >
        ADD
      </button>
    </div>
    <List :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo" />
    <small>Total TODO : {{ totalTodo }}</small>
  </div>
  <footer class="w-full fixed left-0 bottom-0 text-center text-sm">
    © Copyright 2022
  </footer>
</template>

<script>
import List from "./components/List.vue";
export default {
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  computed: {
    totalTodo() {
      return this.todos.length;
    },
  },
  components: {
    List,
  },
  methods: {
    addTodo() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.todo = "";
      this.saveToLocalStorage();
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      this.saveToLocalStorage();
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true;
        }
        return item;
      });
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style></style>
