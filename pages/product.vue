<template>
  <div v-if="pending">Loading...</div>
  <div v-else-if="error">Error: {{ error.message }}</div>
  <ul>
    <li v-for="p in data" :key="p.id">{{ p.name }}</li>
  </ul>
</template>


<script setup>
const { data,pending ,error } = await useFetch('https://localhost:44316/Hitop/Getproduct'
,{
  server: false, 
  watch: [], }
);
</script>