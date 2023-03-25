<template>
  <div class="container pt-4">
    <h2 class="text-lg font-bold mb-4">Our List</h2>
    <div class="flex w-full">
      <input
        @keyup.enter="add"
        v-model="todo"
        type="text"
        class="p-2 w-full rounded-md mr-1 border border-gray-300 bg-gray-50"
      />
      <button
        @click="add"
        class="py-2 px-3 bg-green-500 rounded-md text-white font-medium"
      >
        ADD
      </button>
    </div>
    <List :todos="list" @deleteTodo="deleteTodo" @doneTodo="doneTodo" />
    <small>Total Todo : {{ totalTodo }}</small>
  </div>
</template>

<script>
import { ref, reactive, onMounted, computed, toRefs } from "vue";
import List from "./components/List.vue";
export default {
  components: {
    List,
  },
  setup() {
    const todo = ref("");
    const todos = reactive({
      list: [],
    });

    onMounted(() => {
      const items = localStorage.getItem("todos");
      todos.list = items ? JSON.parse(items) : [];
    });
    const totalTodo = computed(() => {
      return todos.list.length;
    });
    const add = () => {
      todos.list.unshift({
        activity: todo.value,
        isDone: false,
      });
      todo.value = "";
      saveToLocalStorage();
    };
    const deleteTodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      saveToLocalStorage();
    };
    const doneTodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true;
        }
        return item;
      });
      saveToLocalStorage();
    };
    const saveToLocalStorage = () => {
      localStorage.setItem("todos", JSON.stringify(todos.list));
    };
    return {
      todo,
      ...toRefs(todos),
      totalTodo,
      add,
      deleteTodo,
      doneTodo,
      List,
    };
  },
};
</script>

<style></style>
