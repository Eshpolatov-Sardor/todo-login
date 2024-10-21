<script setup lang="ts">
import { ref } from "vue";
import OpenModal from "./OpenModal.vue";
import TodoTextItem from "./TodoListItem.vue";

export interface Todo {
  title: string;
  description: string;
  active: boolean;
}

const ismodalshart = ref<boolean>(false);
const todos = ref<Todo[]>([
  { title: "Sardor", description: "TATU", active: false },
  { title: "Asilbek", description: "TATU", active: false },
  { title: "Bekzod", description: "QDPU", active: false },
]);

const theme = ref<string>("light");

function addtodobutton() {
  ismodalshart.value = true;
}

function closemodal() {
  ismodalshart.value = false;
}

function addtodo(todo: Todo) {
  todos.value.push(todo);
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

function toggleactive(index: number) {
  todos.value[index].active = !todos.value[index].active;
}

function deletetodo(index: number) {
  todos.value.splice(index, 1);
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

function editbutton(index: number) {
  const newtitle = prompt("Edit title", todos.value[index].title);
  const newdescription = prompt(
    "Edit description",
    todos.value[index].description
  );

  if (newtitle !== null && newtitle.trim() !== "") {
    todos.value[index].title = newtitle;
  }

  if (newdescription !== null && newdescription.trim() !== "") {
    todos.value[index].description = newdescription;
  }

  localStorage.setItem("todos", JSON.stringify(todos.value));
}

function setLightTheme() {
  theme.value = "light";
}

function setDarkTheme() {
  theme.value = "dark";
}
</script>

<template>
  <div :class="[theme, 'flex flex-col justify-center items-center']">
    <h1
      @click="addtodobutton"
      class="border border-black p-2 mt-5 rounded-lg cursor-pointer"
    >
      Add Todo
    </h1>

    <div class="w-44 flex justify-between mt-5 gap-2">
      <span
        @click="setLightTheme"
        class="border border-black bg-white text-black w-24 text-center rounded-full cursor-pointer"
      >
        White
      </span>
      <span
        @click="setDarkTheme"
        class="border border-white bg-black text-white w-24 text-center rounded-full cursor-pointer"
      >
        Dark
      </span>
    </div>

    <OpenModal
      v-if="ismodalshart"
      @addtodo="addtodo"
      @closemodal="closemodal"
    />

    <ol>
      <TodoTextItem
        v-for="(item, index) in todos"
        :key="index"
        :todo="item"
        :index="index"
        @toggleactive="toggleactive"
        @deletetodo="deletetodo"
        @editbutton="editbutton"
        @setDarkTheme="setDarkTheme"
      />
    </ol>
  </div>
</template>

<style scoped>
.light {
  background-color: white;
  color: black;
}

.dark {
  background-color: black;
  color: white;
  border: 1px solid white;
  padding-bottom: 310px;
}

</style>
