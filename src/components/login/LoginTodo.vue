<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["logintodo", "showRegister"]);

const email = ref<string>("");
const password = ref<string>("");
function logintodo() {
  emit("logintodo", email.value, password.value);

  const loginData = { email: email.value, password: password.value };
  localStorage.setItem("loginData", JSON.stringify(loginData));

  email.value = "";
  password.value = "";
}
function handleShowRegister() {
  emit("showRegister");
}
</script>

<template>
  <div class="w-full flex justify-center bg-no-repeat bg-black p-10 pb-56">
    <div
      class="flex justify-center items-center border border-white w-96 rounded-3xl"
    >
      <div class="flex flex-col justify-center items-center p-10">
        <h1 class="text-4xl text-white">Login</h1>
        <input
          v-model="email"
          type="text"
          class="text-white border border-white rounded-2xl p-3 mt-14 w-80 bg-opacity-0 bg-slate-900"
          placeholder="email"
        />
        <input
          v-model="password"
          type="password"
          class="text-white border border-white rounded-2xl p-3 mt-4 w-80 bg-opacity-0 bg-slate-900"
          placeholder="password"
        />
        <button
          class="text-black bg-white p-2 w-64 rounded-3xl mt-8"
          @click="logintodo"
        >
          Login
        </button>
        <p class="text-white mt-8">Don't have an account?</p>
        <button class="border-b-2 text-white" @click="handleShowRegister">
          Register
        </button>
      </div>
    </div>
  </div>
</template>
