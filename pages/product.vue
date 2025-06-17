<template>
  <div class="max-w-3xl mx-auto p-4">

    <div class="flex gap-4">
      <select
        v-model="selectedType"
        class="p-3 border border-gray-300 rounded-md bg-white text-gray-700 focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
        <option value="">All</option>
        <option value="Food">Food</option>
        <option value="Drink">Drink</option>
      </select>

      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search products..."
        class="w-full p-3 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
      />
    </div>

    <ul class="mt-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <li
        v-for="p in filteredProducts"
        :key="p.id"
        class="p-4 border rounded-lg hover:shadow-lg transition"
      >
        <h3 class="font-semibold text-lg mb-2">{{ p.name }}</h3>
        <p class="font-semibold text-sm mb-2">{{ 'Description: '+p.description }}</p>
        <p class="text-indigo-600 font-bold">${{ p.price }}</p>
      </li>
    </ul>

    <p v-if="filteredProducts.length === 0" class="mt-4 text-center text-gray-500">
      No products found.
    </p>
    <p v-if="pending" class="mt-4 text-center text-gray-500">
      Loading.......
    </p>
  </div>


</template>


<script setup>

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

watch(searchQuery, () => {
  getProduct()
})

const filteredProducts = computed(() => {
  if (!searchQuery.value && !selectedType.value) return data.value
  return data.value.filter(product =>
    product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    && (!selectedType.value || selectedType.value === '' || product.type === selectedType.value)
  )
})

getProduct()
</script>