<template>
  <div v-if="modelValue" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded shadow-lg w-96">
      <h2 class="text-lg font-bold">{{ product.name }}</h2>
      <p>{{ 'Type: '+product.type }}</p>
      <p>{{ 'Description: '+product.description }}</p>
      <p>{{ 'Price: $'+product.price }}</p>
      <div class="mt-4 text-right">
        <button @click="$emit('update:modelValue', false)" class="px-4 py-2 bg-gray-200 rounded">Close</button>
      </div>
    </div>
  </div>
</template>

<script setup>

  defineProps({
    modelValue: {
      type: Boolean,
      required: true
    },
    product: Object
  })

</script>
