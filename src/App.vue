<script setup lang="ts">
// import { RouterLink, RouterView } from 'vue-router'
import Images from './components/Images.vue'
import Navbar from './components/Navbar.vue'
</script>

<template>
  <link rel="stylesheet" href="/output.css" />
  <Navbar />
  <div class="bg-gray-100 min-h-screen p-4">
    <div id="app" class="mx-auto flex flex-col items-center">
      <header class="mb-8 text-center">
        <h1 class="text-3xl font-bold text-gray-800 mb-2">Responsive Image Gallery</h1>
        <p class="text-gray-500">Click on any image for full-screen preview</p>
      </header>
      <Images />
      <footer class="mt-8 text-center">
        <p class="text-gray-500">© 2025 ---</p>
        <p class="text-gray-500">All rights reserved.</p>
      </footer>
    </div>
  </div>
</template>
