<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["registerodo", "registerUser"]);

const username = ref<string>("");
const email = ref<string>("");
const password = ref<string>("");

function registerodo() {
  emit("registerodo", username.value, email.value, password.value);

  const loginData = {
    username: email.value,
    email: email.value,
    password: password.value,
  };
  localStorage.setItem("loginData", JSON.stringify(loginData));

  username.value = "";
  email.value = "";
  password.value = "";
}

function handleRegister() {
  emit("registerUser", username.value, email.value, password.value);
}
</script>

<template>
  <div class="w-full flex justify-center  bg-no-repeat bg-black p-10 pb-40">
    <div
      class="flex justify-center items-center border border-white w-96 rounded-3xl"
    >
      <div class="flex flex-col justify-center items-center p-10">
        <h1 class="text-4xl text-white">Register</h1>
        <input
          v-model="username"
          type="text"
          class="text-white border border-white rounded-2xl p-3 mt-14 w-80 bg-opacity-0 bg-slate-900"
          placeholder="user name"
        />
        <input
          v-model="email"
          type="text"
          class="text-white border border-white rounded-2xl p-3 mt-4 w-80 bg-opacity-0 bg-slate-900"
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
          @click="registerodo"
        >
        Register
        </button>
        <p class="text-white mt-8">Do you have an account?</p>
        <button class="border-b-2 text-white" @click="handleRegister">
          Login
        </button>
      </div>
    </div>
  </div>
</template>
