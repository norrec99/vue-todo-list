<!-- This example requires Tailwind CSS v2.0+ -->
<template>
  <div>
    <form @submit.prevent="addNewTodo">
      <label class="block text-base font-medium text-gray-700 required"
        >Add Todo</label
      >
      <div class="mt-1">
        <input
          v-model="newTodo"
          type="text"
          class="border-2 border-indigo-200 shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-base border-gray-300 rounded-md p-2"
          placeholder=" Wash the dishes"
        />
      </div>
    </form>

    <ul class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 mt-8">
      <li
        v-for="(todo, index) in todos"
        :key="todo.id"
        class="col-span-1 bg-white rounded-lg shadow divide-y divide-gray-200"
      >
        <div class="w-full flex items-center justify-between p-6 space-x-6">
          <div class="flex-1 truncate">
            <div class="flex items-center space-x-3">
              <h3
                class="text-gray-900 text-sm font-medium truncate"
                :class="{ done: todo.done }"
              >
                {{ todo.name }}
              </h3>
              <span
                v-if="todo.done"
                class="flex-shrink-0 inline-block px-2 py-0.5 text-green-800 text-xs font-medium bg-green-100 rounded-full"
                >Done</span
              >
              <span
                v-else
                class="flex-shrink-0 inline-block px-2 py-0.5 text-green-800 text-xs font-medium bg-red-100 rounded-full"
                >Ongoing</span
              >
            </div>
            <p
              class="mt-1 text-gray-500 text-sm truncate"
              :class="{ done: todo.done }"
            >
              {{ todo.content }}
            </p>
          </div>
          <img
            class="w-10 h-10 bg-gray-300 rounded-full flex-shrink-0"
            :src="todo.imageUrl"
            alt=""
          />
        </div>
        <div>
          <div class="-mt-px flex divide-x divide-gray-200">
            <div class="w-0 flex-1 flex">
              <a
                class="button relative -mr-px w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-bl-lg hover:text-white hover:bg-green-500"
                @click="toggleDone(todo)"
              >
                <CheckIcon class="w-5 h-5 text-black-400" aria-hidden="true" />
                <span class="ml-3">Done</span>
              </a>
            </div>
            <div class="-ml-px w-0 flex-1 flex">
              <a
                class="button relative w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-br-lg hover:text-white hover:bg-yellow-500"
              >
                <PencilIcon class="w-5 h-5 text-black-400" aria-hidden="true" />
                <span class="ml-3">Edit</span>
              </a>
            </div>
            <!-- <EditTodos /> -->

            <div class="-ml-px w-0 flex-1 flex">
              <a
                class="button relative w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-br-lg hover:text-white hover:bg-red-500"
                @click="removeTodo(index)"
              >
                <TrashIcon class="w-5 h-5 text-black-400" aria-hidden="true" />
                <span class="ml-3">Delete</span>
              </a>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
import { CheckIcon, PencilIcon, TrashIcon } from "@heroicons/vue/solid";

const todoNumber = ref(1);
const newTodo = ref("");
const todos = ref([
  {
    name: "Sample Todo 1",
    content: "Wash the dishes",
    done: false,
    imageUrl: "https://github.com/norrec99.png",
  },
  {
    name: "Sample Todo 2",
    content: "Walk the dog",
    done: false,
    imageUrl: "https://github.com/norrec99.png",
  },

  // More todos...
]);

export default {
  components: {
    CheckIcon,
    PencilIcon,
    TrashIcon,
  },
  setup() {
    function incrementTodo() {
      return "No." + todoNumber.value++ + " Todo";
    }
    function addNewTodo() {
      console.log(newTodo.value);
      if (newTodo.value.trim().length > 0) {
        todos.value.push({
          id: Date.now(),
          done: false,
          content: newTodo.value,
          name: incrementTodo(),

          imageUrl: "https://github.com/norrec99.png",
        });
        newTodo.value = "";
      }
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
      // console.log(todo.done);
    }

    function removeTodo(index) {
      // console.log(this.todos[index].done);
      if (this.todos[index].done === true) {
        todos.value.splice(index, 1);
      }
    }

    return {
      todoNumber,
      todos,
      newTodo,
      incrementTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
    };
  },
};
</script>
<style scoped>
.button {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
.required:after {
  content: " *";
  color: red;
}
</style>
