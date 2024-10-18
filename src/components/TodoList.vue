<script setup lang="ts">
import { ref } from "vue";
import OpenModal from './OpenModal.vue';
import TodoTextItem from './TodoTextItem.vue';

export interface Todo{
  title: string,
  description: string,
  active: boolean
}

const ismodalshart = ref(false);
const todos = ref<Todo[]>([
  { title: "Sardor", description: "TATU", active: false },
  { title: "Asilbek", description: "TATU", active: false },
  { title: "Bekzod", description: "QDPU", active: false },
]);

function addtodobutton () {
  ismodalshart.value = true;
};

function closemodal () {
  ismodalshart.value = false;
};

function addtodo(todo: Todo) {
  todos.value.push(todo);
  localStorage.setItem('todos', JSON.stringify(todos.value));
};

function toggleactive (index: number) {
  todos.value[index].active = !todos.value[index].active;
};

function deletetodo (index: number) {
  todos.value.splice(index, 1);
  localStorage.setItem("todos", JSON.stringify(todos.value));
};

function editbutton (index: number) {
  const newtitle = prompt("Edit title", todos.value[index].title);
  const newdescription = prompt("Edit description", todos.value[index].description);

  if (newtitle !== null && newtitle.trim() !== "") {
    todos.value[index].title = newtitle;
  }

  if (newdescription !== null && newdescription.trim() !== "") {
    todos.value[index].description = newdescription;
  }

  localStorage.setItem("todos", JSON.stringify(todos.value));
};
</script>

<template>
  <div class="flex flex-col justify-center items-center">
    <h1
      @click="addtodobutton"
      class="border border-black p-2 mt-5 rounded-lg bg-slate-800 text-yellow-50 cursor-pointer"
    >
      Add Todo
    </h1>
    
    <div v-if="ismodalshart">
      <OpenModal @addtodo="addtodo" @closemodal="closemodal" />
    </div>

    <TodoTextItem
      :todos="todos"
      @toggleactive="toggleactive"
      @deletetodo="deletetodo"
      @editbutton="editbutton"
    />
  </div>
</template>

<style scoped></style>
