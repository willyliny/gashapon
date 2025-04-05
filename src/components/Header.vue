<script setup>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()
const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const navigateToCategory = (categoryId) => {
  router.push(`/category/${categoryId}`)
  isMenuOpen.value = false
}

const isActive = (path) => {
  if (path === '/') {
    return route.path === path
  }
  return route.path.startsWith(path)
}
</script>

<template>
  <header class="bg-white shadow-sm fixed w-full top-0 z-50">
    <nav class="container mx-auto px-4">
      <!-- 主要導航 -->
      <div class="flex justify-between items-center h-16">
        <!-- Logo -->
        <div class="flex items-center">
          <a href="/" class="text-2xl font-bold text-orange-500 hover:text-orange-600 transition-colors">
            Gashapon
          </a>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden lg:flex items-center space-x-1">
          <a href="/" 
             :class="[
               'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
               isActive('/') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
             ]">
            首頁
          </a>
          <button @click="navigateToCategory('ichiban')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
                    isActive('/category/ichiban') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            一番賞
          </button>
          <button @click="navigateToCategory('gashapon')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
                    isActive('/category/gashapon') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            扭蛋
          </button>
          <button @click="navigateToCategory('anime')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
                    isActive('/category/anime') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            動漫周邊
          </button>
          <button @click="navigateToCategory('original')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
                    isActive('/category/original') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            自製商品
          </button>
          <button class="ml-4 bg-orange-500 text-white px-4 py-2 rounded-lg text-sm font-medium hover:bg-orange-600 transition-colors shadow-sm hover:shadow">
            登入
          </button>
        </div>

        <!-- Mobile Menu Button -->
        <button @click="toggleMenu" 
                class="lg:hidden p-2 rounded-lg bg-white hover:text-orange-500 transition-colors">
          <span class="sr-only">選單</span>
          <svg xmlns="http://www.w3.org/2000/svg" 
               class="h-6 w-6 text-gray-600" 
               fill="none" 
               viewBox="0 0 24 24" 
               stroke="currentColor">
            <path v-if="!isMenuOpen" 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M4 6h16M4 12h16M4 18h16" />
            <path v-else 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Mobile Navigation -->
      <div v-show="isMenuOpen" 
           class="lg:hidden py-4 border-t border-gray-100">
        <div class="flex flex-col space-y-2">
          <a href="/" 
             :class="[
               'px-4 py-2 rounded-lg text-sm font-medium transition-colors bg-white',
               isActive('/') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
             ]">
            首頁
          </a>
          <button @click="navigateToCategory('ichiban')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors text-left bg-white',
                    isActive('/category/ichiban') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            一番賞
          </button>
          <button @click="navigateToCategory('gashapon')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors text-left bg-white',
                    isActive('/category/gashapon') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            扭蛋
          </button>
          <button @click="navigateToCategory('anime')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors text-left bg-white',
                    isActive('/category/anime') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            動漫周邊
          </button>
          <button @click="navigateToCategory('original')"
                  :class="[
                    'px-4 py-2 rounded-lg text-sm font-medium transition-colors text-left bg-white',
                    isActive('/category/original') ? 'bg-orange-50 text-orange-500' : 'text-gray-600 hover:text-orange-500'
                  ]">
            自製商品
          </button>
          <button class="mt-4 bg-orange-500 text-white px-4 py-2 rounded-lg text-sm font-medium hover:bg-orange-600 transition-colors shadow-sm hover:shadow">
            登入
          </button>
        </div>
      </div>
    </nav>
  </header>
</template> 