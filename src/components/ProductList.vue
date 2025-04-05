<script setup>
import { ref, computed } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

// 公佈欄消息數據
const announcements = [
  {
    id: 1,
    type: '活動',
    title: '黃金週特別活動開跑！',
    content: '4月29日～5月5日期間，全站商品免運費！',
    date: '2024/04/25',
    isImportant: true
  },
  {
    id: 2,
    type: '新商品',
    title: '【新商品預告】排球少年扭蛋第二彈即將上線',
    content: '預計5月中旬開始販售，敬請期待！',
    date: '2024/04/20'
  },
  {
    id: 3,
    type: '通知',
    title: '系統維護通知',
    content: '5月1日凌晨0:00～2:00將進行系統維護，期間將暫停服務。',
    date: '2024/04/18'
  }
]

// 熱門商品數據
const hotProducts = [
  {
    id: 'volleyball',
    image: '/products/product1.jpg',
    title: '排球少年徽章',
    status: '販售中',
    endDate: '2025/05/13(四) 17:59 截止',
    isNew: true,
    type: 'BOX類型',
    boxCount: 74,
    price: 730,
    shipping: {
      first: 770,
      note: '※運費僅限首次購買，第二次以後的訂單免運費'
    },
    saleTime: {
      start: '2025/02/18(二) 17:00',
      end: '2025/05/13(四) 17:59'
    },
    payment: ['信用卡', 'PayPay', '電子支付'],
    releaseDate: '2025年6月中旬~下旬'
  },
  {
    id: 'yakuza',
    image: '/products/product2.jpg',
    title: '黑道風雲扭蛋',
    status: '已完售',
    endDate: '2025/05/08(四) 16:59 截止',
    isNew: true
  },
  {
    id: 'baseball',
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
        id: 'gee-kawaii',
        image: '/products/ichiban1.jpg',
        title: '吉伊卡哇',
        status: '販售中',
        endDate: '2025/05/13(四) 17:59 截止',
        type: 'BOX類型',
        boxCount: 74,
        price: 730,
        shipping: {
          first: 770,
          note: '※運費僅限首次購買，第二次以後的訂單免運費'
        },
        saleTime: {
          start: '2025/02/18(二) 17:00',
          end: '2025/04/09(三) 17:59'
        },
        payment: ['信用卡', 'PayPay', '電子支付'],
        releaseDate: '2025年6月中旬~下旬'
      }
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
        id: 'volleyball',
        image: '/products/product1.jpg',
        title: '排球少年徽章',
        status: '販售中',
        endDate: '2025/05/13(四) 17:59 截止',
        isNew: true,
        type: 'BOX類型',
        boxCount: 74,
        price: 730,
        shipping: {
          first: 770,
          note: '※運費僅限首次購買，第二次以後的訂單免運費'
        },
        saleTime: {
          start: '2025/02/18(二) 17:00',
          end: '2025/05/13(四) 17:59'
        },
        payment: ['信用卡', 'PayPay', '電子支付'],
        releaseDate: '2025年6月中旬~下旬'
      }
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
      <!-- 公佈欄區域 -->
      <section v-if="!currentCategory" class="mb-32">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-gray-800 mb-4">最新消息</h2>
          <p class="text-gray-600">官方公告 & 活動資訊</p>
        </div>

        <div class="bg-white rounded-2xl shadow-sm overflow-hidden">
          <div class="divide-y divide-gray-100">
            <div v-for="announcement in announcements" 
                 :key="announcement.id"
                 class="group hover:bg-orange-50/50 transition-colors duration-300">
              <div class="p-6">
                <div class="flex items-start gap-4">
                  <!-- 消息類型標籤 -->
                  <div :class="[
                    'px-3 py-1 rounded-full text-sm font-medium whitespace-nowrap',
                    {
                      'bg-red-50 text-red-500': announcement.type === '活動',
                      'bg-blue-50 text-blue-500': announcement.type === '新商品',
                      'bg-gray-50 text-gray-500': announcement.type === '通知'
                    }
                  ]">
                    {{ announcement.type }}
                  </div>

                  <!-- 消息內容 -->
                  <div class="flex-1">
                    <div class="flex items-center gap-2 mb-2">
                      <h3 class="text-lg font-bold text-gray-800">
                        {{ announcement.title }}
                      </h3>
                      <span v-if="announcement.isImportant" 
                            class="bg-red-50 text-red-500 px-2 py-0.5 rounded text-xs font-medium">
                        重要
                      </span>
                    </div>
                    <p class="text-gray-600 mb-2">{{ announcement.content }}</p>
                    <div class="text-sm text-gray-400">{{ announcement.date }}</div>
                  </div>

                  <!-- 箭頭圖標 -->
                  <div class="text-gray-400 group-hover:text-orange-500 transition-colors">
                    <svg xmlns="http://www.w3.org/2000/svg" 
                         class="h-5 w-5" 
                         fill="none" 
                         viewBox="0 0 24 24" 
                         stroke="currentColor">
                      <path stroke-linecap="round" 
                            stroke-linejoin="round" 
                            stroke-width="2" 
                            d="M9 5l7 7-7 7" />
                    </svg>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

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