<template>
  <section
    class="min-h-screen flex flex-col justify-center items-center bg-gradient-to-br from-indigo-500 via-purple-600 to-pink-500 text-white px-6 py-20"
  >
    <h1
      class="text-4xl sm:text-5xl md:text-6xl font-extrabold mb-6 text-center drop-shadow-lg leading-tight max-w-4xl"
    >
      Welcome to <span class="text-yellow-300">Ecommerce</span>
    </h1>
    <NuxtLink
      to="/product"
      class="bg-yellow-400 text-indigo-900 font-bold py-3 px-8 rounded-lg shadow-lg hover:bg-yellow-300 transition"
    >
      Go Find Product
    </NuxtLink>
  </section>
</template>



