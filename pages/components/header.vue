<template>
  <header class="bg-white shadow sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 py-4 flex items-center justify-between">
      
      <!-- Shop Name -->
      <NuxtLink to="/"><h1 class="text-xl font-bold text-indigo-600">Hitop</h1></NuxtLink>


      <!-- Menu -->
      <nav class="hidden md:flex gap-6 text-gray-700 font-medium">
        <NuxtLink to="/" class="hover:text-indigo-600 transition">Home</NuxtLink>
        <NuxtLink to="/product" class="hover:text-indigo-600 transition">Products</NuxtLink>
      </nav>

      <!-- Mobile Menu Toggle -->
      <button class="md:hidden" @click="toggleMenu">
        <svg class="w-6 h-6 text-gray-700" fill="none" stroke="currentColor" stroke-width="2"
             viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round">
          <path v-if="!mobileOpen" d="M4 6h16M4 12h16M4 18h16" />
          <path v-else d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <!-- Mobile Menu -->
    <div v-if="mobileOpen" class="md:hidden bg-white border-t border-gray-200 px-4 py-4">
      <NuxtLink to="/" class="block py-2 text-gray-700 hover:text-indigo-600" @click="closeMenu">Home</NuxtLink>
      <NuxtLink to="/product" class="block py-2 text-gray-700 hover:text-indigo-600" @click="closeMenu">Products</NuxtLink>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const mobileOpen = ref(false)

function toggleMenu() {
  mobileOpen.value = !mobileOpen.value
}

function closeMenu() {
  mobileOpen.value = false
}
</script>
