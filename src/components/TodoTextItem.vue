<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

interface Todo {
  title: string;
  description: string;
  active: boolean;
}

const props = defineProps<{
  todos: Todo[]
}>();

const emit = defineEmits(['toggleactive', 'deletetodo','editbutton']);

function toggleactive(index: number) {
  emit('toggleactive', index);
}

function deletetodo(index: number) {
  emit('deletetodo', index);
}
function editbutton(index: number) {
  emit('editbutton', index);
}
</script>


<template>
  <ol>
    <li
      v-for="(item, index) in todos"
      :key="index"
      class="flex justify-between items-center w-72 mt-5 border border-black p-2 rounded-lg"
      :class="{ 'line-through': item.active }"
    >
      <span>
        <p>{{ item.title }}</p>
        <p>{{ item.description }}</p>
      </span>
      <span class="flex items-center gap-2">
        <input
          class="w-3 h-3 border border-black cursor-pointer"
          type="checkbox"
          :checked="item.active"
          @change="toggleactive(index)"
        />
        <button @click="deletetodo(index)">
          <svg
            width="22"
            height="22"
            viewBox="0 0 22 22"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M1 5H21M9 10V15M13 10V15M3 5H19L17.42 19.22C17.3658 19.7094 17.1331 20.1616 16.7663 20.49C16.3994 20.8184 15.9244 21 15.432 21H6.568C6.07564 21 5.60056 20.8184 5.23375 20.49C4.86693 20.1616 4.63416 19.7094 4.58 19.22L3 5ZM6.345 2.147C6.50675 1.80397 6.76271 1.514 7.083 1.31091C7.4033 1.10782 7.77474 0.999996 8.154 1H13.846C14.2254 0.999806 14.5971 1.10755 14.9176 1.31064C15.2381 1.51374 15.4942 1.80381 15.656 2.147L17 5H5L6.345 2.147V2.147Z"
              stroke="#FF4545"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            ></path>
          </svg>
        </button>
        <button @click="editbutton(index)">
          <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="20" height="20" viewBox="0 0 24 24">
              <path d="M 18 2 L 15.585938 4.4140625 L 19.585938 8.4140625 L 22 6 L 18 2 z M 14.076172 5.9238281 L 3 17 L 3 21 L 7 21 L 18.076172 9.9238281 L 14.076172 5.9238281 z"></path>
          </svg>
        </button>
      </span>
    </li>
  </ol>
</template>

<style scoped></style>
