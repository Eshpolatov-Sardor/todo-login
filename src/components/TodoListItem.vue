<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import type { Todo } from "./TodoList.vue";
import Delete from "./svg/Delete.vue";
import Edit from "./svg/Edit.vue";

const props = defineProps<{
  todo: Todo;
  index: number;
}>();

const emit = defineEmits<{
  (e: "toggleactive", index: number): void;
  (e: "deletetodo", index: number): void;
  (e: "editbutton", index: number): void;
}>();

function toggleactive() {
  emit("toggleactive", props.index);
}

function deletetodo() {
  emit("deletetodo", props.index);
}

function editbutton() {
  emit("editbutton", props.index);
}
</script>

<template>
  <li
    class="flex justify-between items-center w-72 mt-5 border p-2 rounded-lg"
    :class="{ 'line-through': todo.active }"
  >
    <span>
      <p>{{ todo.title }}</p>
      <p>{{ todo.description }}</p>
    </span>

    <span class="flex items-center gap-2">
      <input
        class="w-3 h-3 border cursor-pointer"
        type="checkbox"
        :checked="todo.active"
        @change="toggleactive"
      />

      <Delete @click="deletetodo" class="cursor-pointer" />
      <Edit @click="editbutton" class="cursor-pointer" />
    </span>
  </li>
</template>

<style scoped>
li {
  background-color: white;
  color: black;
}

.dark li {
  background-color: black;
  color: white;
}
</style>
