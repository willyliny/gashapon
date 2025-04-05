<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <header class="bg-white shadow-md fixed w-full top-0 z-50">
    <nav class="container mx-auto px-4 py-4">
      <div class="flex justify-between items-center">
        <!-- Logo -->
        <div class="flex items-center">
          <a href="/" class="text-xl sm:text-2xl font-bold text-orange-500 hover:text-orange-600 transition-colors">
            Gashapon
          </a>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden lg:flex items-center space-x-8">
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">首頁</a>
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">商品</a>
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">關於我們</a>
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">聯絡我們</a>
          <button class="bg-orange-500 text-white px-4 sm:px-6 py-2 rounded-full hover:bg-orange-600 transition-colors shadow-md hover:shadow-lg">
            登入
          </button>
        </div>

        <!-- Tablet Navigation -->
        <div class="hidden md:flex lg:hidden items-center space-x-4">
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">首頁</a>
          <a href="#" class="text-gray-600 hover:text-orange-500 transition-colors">商品</a>
          <button @click="toggleMenu" class="text-gray-600 hover:text-orange-500 transition-colors">
            <span class="sr-only">選單</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
        </div>

        <!-- Mobile Menu Button -->
        <button @click="toggleMenu" class="md:hidden text-gray-600 hover:text-orange-500 transition-colors">
          <span class="sr-only">選單</span>
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Mobile/Tablet Navigation Dropdown -->
      <div v-show="isMenuOpen" 
           class="lg:hidden mt-4 pb-4 border-t border-gray-100"
           @click="isMenuOpen = false">
        <div class="flex flex-col space-y-4 pt-4">
          <div class="md:hidden">
            <a href="#" class="block text-gray-600 hover:text-orange-500 transition-colors">首頁</a>
            <a href="#" class="block text-gray-600 hover:text-orange-500 transition-colors mt-4">商品</a>
          </div>
          <a href="#" class="block text-gray-600 hover:text-orange-500 transition-colors">關於我們</a>
          <a href="#" class="block text-gray-600 hover:text-orange-500 transition-colors">聯絡我們</a>
          <button class="bg-orange-500 text-white px-4 py-2 rounded-full hover:bg-orange-600 transition-colors shadow-md hover:shadow-lg w-full md:w-auto">
            登入
          </button>
        </div>
      </div>
    </nav>
  </header>
</template> 