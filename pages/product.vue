<template>
  <div class="max-w-6xl mx-auto px-4 py-8">

    <!-- Filters -->
    <div class="flex flex-col md:flex-row gap-4 items-center mb-6">

      <!-- Select Type -->
      <select
        v-model="selectedType"
        class="w-full md:w-48 px-4 py-3 border border-gray-300 rounded-md bg-white text-gray-700 shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        <option value="">All</option>
        <option value="Food">Food</option>
        <option value="Drink">Drink</option>
      </select>

      <!-- Search by name  -->
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search products..."
        class="w-full px-4 py-3 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500"
      />
    </div>

    <!-- Product List -->
    <ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <li
        v-for="p in filteredProducts"
        :key="p.id"
        class="p-5 border rounded-lg hover:shadow-xl hover:bg-indigo-50 transition cursor-pointer"
        @click="openDialog(p)"
      >
        <h3 class="font-semibold text-lg mb-1 text-gray-800">{{ p.name }}</h3>
        <p class="text-sm text-gray-600 mb-2">Description: {{ p.description }}</p>
        <p class="text-indigo-600 font-bold text-lg">${{ p.price }}</p>
      </li>
    </ul>

    <!-- No Product -->
    <p v-if="filteredProducts.length === 0 && !pending" class="mt-10 text-center text-gray-400 text-lg">
      No products found.
    </p>

    <!-- Loading -->
    <p v-if="pending" class="mt-10 text-center text-indigo-500 text-lg animate-pulse">
      Loading...
    </p>

    <!-- Dialog -->
    <ProductDetailDialog
      v-model="showDialog"
      :product="selectProduct"
    />
  </div>
</template>


<script setup>

import ProductDetailDialog from './components/productDetailDialog.vue'

// Dialog visibility
const showDialog = ref(false)
// Select product
const selectProduct = ref(null)

function openDialog(product) {
  selectProduct.value = product;
  showDialog.value = true;
}


// Search
const searchQuery = ref('')
const selectedType = ref('')
const data = ref([])
const pending = ref(false)
const error = ref(null)


const getProduct = async () => {
  pending.value = true
  error.value = null
  try {
    const result = await $fetch('https://localhost:44316/Hitop/Getproduct', {
      params: {
        search: searchQuery.value
      }
    })
    data.value = result
  } catch (err) {
    error.value = err
  } finally {
    pending.value = false
  }
}

// When Search change
watch(searchQuery, () => {
  getProduct()
})


//Products filter By type and name
const filteredProducts = computed(() => {
  if (!searchQuery.value && !selectedType.value) return data.value
  return data.value.filter(product =>
    product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    && (!selectedType.value || selectedType.value === '' || product.type === selectedType.value)
  )
})

getProduct()
</script>