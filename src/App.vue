<template>
  <HelloWorld :label="label" :user="user" />
  <button @click="changeName">change</button>
</template>

<script>
import { reactive, ref } from "@vue/reactivity";
import HelloWorld from "./components/HelloWorld.vue";
export default {
  components: {
    HelloWorld,
  },
  setup() {
    const label = ref("Biodata");
    const user = reactive({
      name: "agus",
      age: 24,
    });
    const changeName = () => {
      user.name = "asep";
    };
    return {
      label,
      user,
      changeName,
    };
  },
};
</script>

<style></style>
