<script setup lang="ts">
import { ref, defineEmits } from "vue";

const title = ref<string>("");
const description = ref<string>("");
const emit = defineEmits(["addtodo", "closemodal"]);

function submit() {
  if (title.value !== "" && description.value !== "") {
    emit("addtodo", {
      title: title.value,
      description: description.value,
      active: false,
    });
    title.value = "";
    description.value = "";
    emit("closemodal");
  } else if (title.value !== "" && description.value === "") {
    alert("descriptionga ham malumot kiriting");
  } else {
    alert("titlega ham malumot kiriting");
  }
}
</script>

<template>
  <div class="bg-white p-5 rounded shadow-lg absolute mt-28 -ml-18">
    <form @submit.prevent="submit">
      <label for="title" class="block font-semibold mb-2 text-red-600">Title:</label>
      <input
        type="title"
        v-model="title"
        class="border p-2 w-full rounded mb-4 text-red-600"
        placeholder="Enter Title"
      />

      <label for="description" class="block font-semibold mb-2 text-red-600"
        >Description:</label
      >
      <input
        type="title"
        v-model="description"
        class="border p-2 w-full rounded mb-4 text-red-600"
        placeholder="Enter Description"
      />

      <div class="flex justify-end space-x-2">
        <button type="submit" class="bg-blue-600 title-white px-4 py-2 rounded">
          Add
        </button>
        <button
          type="button"
          @click="$emit('closemodal')"
          class="bg-gray-300 px-4 py-2 rounded"
        >
          Close
        </button>
      </div>
    </form>
  </div>
</template>

<style scoped></style>
