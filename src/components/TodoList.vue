<!-- This example requires Tailwind CSS v2.0+ -->
<template>
  <div>
    <form @submit.prevent="addNewTodo">
      <label class="block text-sm font-medium text-gray-700">Add Todo</label>
      <div class="mt-1">
        <input
          v-model="newTodo"
          type="text"
          class="border-2 border-indigo-200 shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md"
          placeholder=" Wash the dishes"
        />
      </div>
    </form>

    <ul class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-1 mt-8">
      <li
        v-for="todo in todos"
        :key="todo.id"
        class="col-span-1 bg-white rounded-lg shadow divide-y divide-gray-200"
      >
        <div class="w-full flex items-center justify-between p-6 space-x-6">
          <div class="flex-1 truncate">
            <div class="flex items-center space-x-3">
              <h3 class="text-gray-900 text-sm font-medium truncate">
                {{ todo.name }}
              </h3>
              <span
                class="flex-shrink-0 inline-block px-2 py-0.5 text-green-800 text-xs font-medium bg-green-100 rounded-full"
                >{{ todo.role }}</span
              >
            </div>
            <p class="mt-1 text-gray-500 text-sm truncate">
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
                :href="`mailto:${todo.email}`"
                class="relative -mr-px w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-bl-lg hover:text-gray-500"
              >
                <MailIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
                <span class="ml-3">Done</span>
              </a>
            </div>
            <div class="-ml-px w-0 flex-1 flex">
              <a
                :href="`tel:${todo.telephone}`"
                class="relative w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-br-lg hover:text-gray-500"
              >
                <PhoneIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
                <span class="ml-3">Edit</span>
              </a>
            </div>
            <div class="-ml-px w-0 flex-1 flex">
              <a
                :href="`tel:${todo.telephone}`"
                class="relative w-0 flex-1 inline-flex items-center justify-center py-4 text-sm text-gray-700 font-medium border border-transparent rounded-br-lg hover:text-gray-500"
              >
                <PhoneIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
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
import { MailIcon, PhoneIcon } from "@heroicons/vue/solid";

const newTodo = ref("");
const todos = ref([
  {
    name: "Jane Cooper",
    content: "Regional Paradigm Technician",
    role: "Admin",
    email: "janecooper@example.com",
    telephone: "+1-202-555-0170",
    imageUrl:
      "https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60",
  },

  // More todos...
]);

export default {
  components: {
    MailIcon,
    PhoneIcon,
  },
  setup() {
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
        name: "Jane Cooper",
        role: "Admin",
        imageUrl:
          "https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60",
      });
      newTodo.value = "";
    }
    return {
      todos,
      newTodo,
      addNewTodo,
    };
  },
};
</script>
