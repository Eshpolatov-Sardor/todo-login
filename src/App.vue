<script setup lang="ts">
import { ref } from "vue";
import LoginTodo from "./components/login/LoginTodo.vue";
import RegisterTodo from "./components/login/RegisterTodo.vue";
import TodoListVue from "./components/TodoList.vue";

const isLoggedIn = ref<boolean>(false);
const showLogin = ref<boolean>(true);
const showRegister = ref<boolean>(false);

const validCredentials = {
  username: "sardor",
  email: "user@gmail.com",
  password: "123",
};

function logintodo(email: string, password: string) {
  if (
    email === validCredentials.email &&
    password === validCredentials.password
  ) {
    isLoggedIn.value = true;
    showLogin.value = false;
    showRegister.value = false;
  } else {
    alert("Invalid login credentials!");
  }
}
function registerodo(username: string, email: string, password: string) {
  if (
    username === validCredentials.username &&
    email === validCredentials.email &&
    password === validCredentials.password
  ) {
    isLoggedIn.value = true;
    showLogin.value = false;
    showRegister.value = false;
  } else {
    alert("Invalid login credentials!");
  }
}

function showRegisterForm() {
  showLogin.value = false;
  showRegister.value = true;
}
function registerUser() {
  showRegister.value = false;
  showLogin.value = true;
}
</script>

<template>
  <div>
    <LoginTodo
      v-if="showLogin"
      @logintodo="logintodo"
      @showRegister="showRegisterForm"
    />

    <RegisterTodo
      v-if="showRegister"
      @registerUser="registerUser"
      @registerodo="registerodo"
    />

    <TodoListVue v-if="isLoggedIn" />
  </div>
</template>
