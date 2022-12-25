<template>
  <div class="pt-4">
    <ul v-for="(todo, index) in todos" :key="index">
      <div class="flex justify-between mx-4 mb-2 items-center">
        <div class="flex justify-start">
          <li v-if="todo.isDone" class="border-b-2">
            <del>{{ todo.activity }}</del>
          </li>
          <li v-else>{{ todo.activity }}</li>
        </div>
        <div class="flex justify-end">
          <button
            @click="doneTodo(index)"
            class="py-2 px-2 mr-1 bg-blue-600 rounded-md text-white font-medium"
          >
            Done
          </button>
          <button
            class="py-2 px-3 bg-red-600 text-white rounded-md font-medium"
            @click="deleteTodo(index)"
          >
            Delete
          </button>
        </div>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },
  methods: {
    deleteTodo(index) {
      this.$emit("deleteTodo", index);
    },
    doneTodo(index) {
      this.$emit("doneTodo", index);
    },
  },
};
</script>

<style></style>
