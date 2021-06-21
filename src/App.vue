<template>
  <NavbarHeader />
  <div class="w-full flex justify-center mt-8">
    <TodoList />
  </div>
</template>

<script>
import NavbarHeader from "./components/NavbarHeader";
import TodoList from "./components/TodoList";
export default {
  name: "App",
  components: {
    NavbarHeader,
    TodoList,
  },
};
</script>

<style></style>
