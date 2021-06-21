<template>
  <NavbarHeader />
  <div class="w-full flex justify-center mt-8">
    <TodoList />
  </div>
  <Todo />
</template>

<script>
import Todo from "./components/Todo";
import NavbarHeader from "./components/NavbarHeader";
import TodoList from "./components/TodoList";
export default {
  name: "App",
  components: {
    Todo,
    NavbarHeader,
    TodoList,
  },
};
</script>

<style></style>
