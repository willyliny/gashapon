<script setup>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import HeroCarousel from './components/HeroCarousel.vue'
import ProductList from './components/ProductList.vue'
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <Header />
    
    <!-- Main Content -->
    <main class="flex-grow">
      <router-view></router-view>
    </main>

    <Footer />
  </div>
</template>

<style scoped>
/* 移除舊的樣式，完全使用 Tailwind */
</style>
