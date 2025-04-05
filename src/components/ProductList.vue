<script setup>
import { ref, computed } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

// 熱門商品數據
const hotProducts = [
  {
    id: 1,
    image: '/products/product1.jpg',
    title: '排球少年扭蛋',
    status: '販售中',
    endDate: '2025/05/13(四) 17:59 截止',
    isNew: true
  },
  {
    id: 2,
    image: '/products/product2.jpg',
    title: '黑道風雲扭蛋',
    status: '已完售',
    endDate: '2025/05/08(四) 16:59 截止',
    isNew: true
  },
  {
    id: 3,
    image: '/products/product3.jpg',
    title: '胖球大聯盟扭蛋',
    status: '截止',
    endDate: '2025/05/08(四) 17:59 截止',
    isNew: true
  }
]

// 分類商品數據
const categories = [
  {
    id: 'ichiban',
    title: '一番賞',
    description: '最新一番賞商品都在這裡！',
    products: [
      {
        id: 1,
        image: '/products/ichiban1.jpg',
        title: '海賊王一番賞',
        status: '販售中',
        endDate: '2025/05/13(四) 17:59 截止'
      },
      // 可以添加更多商品...
    ]
  },
  {
    id: 'gashapon',
    title: '扭蛋',
    description: '各式各樣有趣的扭蛋！',
    products: [
      {
        id: 1,
        image: '/products/gashapon1.jpg',
        title: '動物系列扭蛋',
        status: '販售中',
        endDate: '2025/05/13(四) 17:59 截止'
      },
      // 可以添加更多商品...
    ]
  },
  {
    id: 'anime',
    title: '動漫周邊',
    description: '精選動漫周邊商品！',
    products: [
      {
        id: 1,
        image: '/products/anime1.jpg',
        title: '動漫限定周邊',
        status: '販售中',
        endDate: '2025/05/13(四) 17:59 截止'
      },
      // 可以添加更多商品...
    ]
  },
  {
    id: 'original',
    title: '自製商品',
    description: '獨家原創商品！',
    products: [
      {
        id: 1,
        image: '/products/original1.jpg',
        title: '原創限定商品',
        status: '即將上線',
        endDate: '2025/05/13(四) 17:59 截止'
      },
      // 可以添加更多商品...
    ]
  }
]

// 根據路由參數獲取當前類別
const currentCategory = computed(() => {
  const categoryId = route.params.categoryId
  if (!categoryId) return null
  return categories.find(category => category.id === categoryId)
})

// 只顯示當前類別的產品
const filteredCategories = computed(() => {
  if (!currentCategory.value) return categories
  return [currentCategory.value]
})

const goToDetail = (productId) => {
  router.push(`/product/${productId}`)
}

const getStatusStyle = (status) => {
  switch (status) {
    case '販售中':
      return {
        tag: 'bg-green-50 text-green-500',
        badge: '販售中',
        buttonStyle: 'bg-green-500 hover:bg-green-600 text-white',
        buttonText: '立即購買'
      }
    case '即將上線':
      return {
        tag: 'bg-blue-50 text-blue-500',
        badge: '即將上線',
        buttonStyle: 'bg-blue-500 hover:bg-blue-600 text-white',
        buttonText: '預約購買'
      }
    case '已完售':
      return {
        tag: 'bg-gray-50 text-gray-500',
        badge: '已完售',
        buttonStyle: 'bg-gray-300 text-gray-500 cursor-not-allowed',
        buttonText: '已售完'
      }
    case '截止':
      return {
        tag: 'bg-red-50 text-red-500',
        badge: '截止',
        buttonStyle: 'bg-gray-300 text-gray-500 cursor-not-allowed',
        buttonText: '已結束'
      }
  }
}
</script>

<template>
  <div class="bg-gray-100 py-20">
    <div class="container mx-auto px-4 max-w-7xl">
      <!-- 熱門商品區域 -->
      <section v-if="!currentCategory" class="mb-32">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-gray-800 mb-4">熱門販售中</h2>
          <p class="text-gray-600">網路限定！推薦商品在這裡！</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="product in hotProducts" 
               :key="product.id"
               class="group bg-white rounded-lg overflow-hidden shadow-md hover:shadow-xl transition-all duration-300">
            <!-- 商品圖片容器 -->
            <div class="relative w-full h-[280px] bg-gray-50 flex items-center justify-center p-6">
              <!-- 狀態標籤 -->
              <div :class="[
                'absolute top-4 left-0 py-1.5 px-5 font-medium z-10 rounded-r-full text-sm',
                getStatusStyle(product.status).tag
              ]">
                {{ getStatusStyle(product.status).badge }}
                <span class="ml-1" v-if="product.status === '販售中'">🟢</span>
                <span class="ml-1" v-else-if="product.status === '即將上線'">⏳</span>
                <span class="ml-1" v-else-if="product.status === '已完售'">🔚</span>
                <span class="ml-1" v-else-if="product.status === '截止'">⛔</span>
              </div>
              
              <!-- 商品圖片 -->
              <img :src="product.image" 
                   :alt="product.title"
                   class="max-w-full max-h-full w-auto h-auto object-contain transition-transform duration-300 group-hover:scale-105">
            </div>

            <!-- 商品信息 -->
            <div class="p-6">
              <h3 class="text-lg font-bold text-gray-800 mb-3 line-clamp-2 min-h-[3.5rem]">
                {{ product.title }}
              </h3>
              
              <!-- 時間信息 -->
              <div class="flex items-center gap-2 text-gray-500 mb-6">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                <span class="text-sm">{{ product.endDate }}</span>
              </div>

              <!-- 購買按鈕 -->
              <button @click="goToDetail(product.id)"
                      :class="[
                        'w-full py-3 rounded-lg font-bold transition-all duration-300 flex items-center justify-center gap-2',
                        getStatusStyle(product.status).buttonStyle
                      ]"
                      :disabled="product.status === '已完售' || product.status === '截止'">
                <span>{{ getStatusStyle(product.status).buttonText }}</span>
                <svg v-if="product.status === '販售中' || product.status === '即將上線'"
                     xmlns="http://www.w3.org/2000/svg" 
                     class="h-5 w-5" 
                     fill="none" 
                     viewBox="0 0 24 24" 
                     stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- 分類商品區域 -->
      <section v-for="category in filteredCategories" 
               :key="category.id"
               class="mb-32">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-gray-800 mb-4">{{ category.title }}</h2>
          <p class="text-gray-600">{{ category.description }}</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="product in category.products" 
               :key="product.id"
               class="group bg-white rounded-lg overflow-hidden shadow-md hover:shadow-xl transition-all duration-300">
            <!-- 商品圖片容器 -->
            <div class="relative w-full h-[280px] bg-gray-50 flex items-center justify-center p-6">
              <!-- 狀態標籤 -->
              <div :class="[
                'absolute top-4 left-0 py-1.5 px-5 font-medium z-10 rounded-r-full text-sm',
                getStatusStyle(product.status).tag
              ]">
                {{ getStatusStyle(product.status).badge }}
                <span class="ml-1" v-if="product.status === '販售中'">🟢</span>
                <span class="ml-1" v-else-if="product.status === '即將上線'">⏳</span>
                <span class="ml-1" v-else-if="product.status === '已完售'">🔚</span>
                <span class="ml-1" v-else-if="product.status === '截止'">⛔</span>
              </div>
              
              <!-- 商品圖片 -->
              <img :src="product.image" 
                   :alt="product.title"
                   class="max-w-full max-h-full w-auto h-auto object-contain transition-transform duration-300 group-hover:scale-105">
            </div>

            <!-- 商品信息 -->
            <div class="p-6">
              <h3 class="text-lg font-bold text-gray-800 mb-3 line-clamp-2 min-h-[3.5rem]">
                {{ product.title }}
              </h3>
              
              <!-- 時間信息 -->
              <div class="flex items-center gap-2 text-gray-500 mb-6">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                <span class="text-sm">{{ product.endDate }}</span>
              </div>

              <!-- 購買按鈕 -->
              <button @click="goToDetail(product.id)"
                      :class="[
                        'w-full py-3 rounded-lg font-bold transition-all duration-300 flex items-center justify-center gap-2',
                        getStatusStyle(product.status).buttonStyle
                      ]"
                      :disabled="product.status === '已完售' || product.status === '截止'">
                <span>{{ getStatusStyle(product.status).buttonText }}</span>
                <svg v-if="product.status === '販售中' || product.status === '即將上線'"
                     xmlns="http://www.w3.org/2000/svg" 
                     class="h-5 w-5" 
                     fill="none" 
                     viewBox="0 0 24 24" 
                     stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style> 