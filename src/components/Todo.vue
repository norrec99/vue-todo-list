<template>
  <h1>Todo List</h1>
  <div class="w-full flex justify-center">
    <form @submit.prevent="addNewTodo">
      <label class="">Add Todo</label>
      <input
        v-model="newTodo"
        class="border-2 border-indigo-600"
        type="text"
        name="newTodo"
      />
    </form>
  </div>
  <button @click="markAllDone">Mark All Done</button>
  <div class="w-full flex justify-center">
    <ul class="list-inside bg-rose-200">
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 class="todo" @click="toggleDone(todo)" :class="{ done: todo.done }">
          {{ todo.content }}
        </h3>
        <button
          @click="removeTodo(index)"
          class="bg-gradient-to-r from-green-400 to-blue-500 hover:from-pink-500 hover:to-yellow-500 mt-5 h-10"
        >
          Remove
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function toggleDone(todo) {
      todo.done = !todo.done;
      console.log(todo.done);
    }

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => {
        todo.done = true;
      });
    }
    return {
      addNewTodo,
      newTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  },
};
</script>

<style>
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
