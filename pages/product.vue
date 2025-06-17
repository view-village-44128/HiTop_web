<template>
  <div v-if="pending">Loading...</div>
  <div v-else-if="error">Error: {{ error.message }}</div>
  <ul>
    <li v-for="p in data" :key="p.id">{{ p.name }}</li>
  </ul>

  <div class="max-w-3xl mx-auto p-4">
    <input
      v-model="searchQuery"
      type="text"
      placeholder="Search products..."
      class="w-full p-3 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
    />

    <ul class="mt-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <li
        v-for="p in data"
        :key="p.id"
        class="p-4 border rounded-lg hover:shadow-lg transition"
      >
        <h3 class="font-semibold text-lg mb-2">{{ p.name }}</h3>
        <p class="text-indigo-600 font-bold">${{ p.code }}</p>
      </li>
    </ul>

    <p v-if="filteredProducts.length === 0" class="mt-4 text-center text-gray-500">
      No products found.
    </p>
  </div>


</template>


<script setup>
const { data,pending ,error } = await useFetch('https://localhost:44316/Hitop/Getproduct'
,{
  server: false, 
  watch: [], }
);

const searchQuery = ref('')

const products = ref([
  { id: 1, name: 'Apple iPhone 13', price: 999 },
  { id: 2, name: 'Samsung Galaxy S21', price: 899 },
  { id: 3, name: 'Google Pixel 6', price: 799 },
  { id: 4, name: 'OnePlus 9 Pro', price: 969 },
])


const filteredProducts = computed(() => {
  if (!searchQuery.value) return products.value
  return products.value.filter(product =>
    product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})


</script>