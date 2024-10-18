<script setup lang="ts">
import { ref, defineEmits } from 'vue';

const title=ref("")
const description=ref("")
const emit = defineEmits(['addtodo', 'closemodal']);

const submit = () => {
  if(title.value!=="" && description.value!==""){
    emit('addtodo', { title: title.value, description: description.value, active: false });
    title.value = '';
    description.value = '';
    emit('closemodal');
  }
  else if(title.value!=="" && description.value===""){
    alert("descriptionga ham malumot kiriting")
  }
  else{
    alert("titlega ham malumot kiriting")
  }
};
</script>

<template>
  <div class="bg-white p-5 rounded shadow-lg absolute mt-5 -ml-28">
    <form @submit.prevent="submit">
      <label for="title" class="block font-semibold mb-2">Title:</label>
      <input
        type="title"
        v-model="title"
        class="border p-2 w-full rounded mb-4"
        placeholder="Enter Title"
      />

      <label for="description" class="block font-semibold mb-2">Description:</label>
      <input
        type="title"
        v-model="description"
        class="border p-2 w-full rounded mb-4"
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
