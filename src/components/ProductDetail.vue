<script setup>
import { ref } from 'vue'

// 商品基本信息
const productInfo = {
  title: '【特典】G8卡哇',
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

// 獎項數據
const prizes = [
  {
    rank: 'A賞',
    name: '亞克力時鐘',
    image: '/prizes/prize-a.png',
    probability: '7.18%',
    description: '精美亞克力材質時鐘，附帶精美人物插畫'
  },
  {
    rank: 'B賞',
    name: '麻婆拉麵碗',
    image: '/prizes/prize-b.png',
    probability: '7.14%',
    description: '特製麻婆拉麵碗，附帶精美圖案'
  },
  {
    rank: 'C賞',
    name: '馬克杯',
    image: '/prizes/prize-c.png',
    probability: '7.14%',
    description: '精美馬克杯，附帶角色圖案'
  },
  {
    rank: 'D賞',
    name: '壓克力吊飾',
    image: '/prizes/prize-d.png',
    probability: '7.14%',
    description: '可愛壓克力吊飾'
  },
  {
    rank: 'E賞',
    name: '迷你角色立牌',
    image: '/prizes/prize-e.png',
    probability: '7.14%',
    description: '迷你尺寸角色立牌'
  },
  {
    rank: 'F賞',
    name: '徽章套組',
    image: '/prizes/prize-f.png',
    probability: '7.14%',
    description: '精美徽章套組'
  }
]

// 購買數量
const quantity = ref(1)

// 增加數量
const increaseQuantity = () => {
  if (quantity.value < 74) {
    quantity.value++
  }
}

// 減少數量
const decreaseQuantity = () => {
  if (quantity.value > 1) {
    quantity.value--
  }
}
</script>

<template>
  <div class="bg-gray-50 min-h-screen pt-20 pb-12">
    <div class="container mx-auto px-4 max-w-6xl">
      <!-- 商品標題 -->
      <div class="bg-white rounded-2xl p-8 mb-8 shadow-sm">
        <h1 class="text-2xl font-medium text-gray-700 mb-6">{{ productInfo.title }}</h1>
        
        <!-- 基本信息 -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <div class="space-y-5">
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">類型</span>
              <span class="font-medium text-gray-600">{{ productInfo.type }}</span>
            </div>
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">BOX數量</span>
              <span class="font-medium text-gray-600">{{ productInfo.boxCount }}枚</span>
            </div>
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">單價</span>
              <span class="font-medium text-gray-600">{{ productInfo.price }}元</span>
            </div>
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">運費</span>
              <div class="text-right">
                <div class="font-medium text-gray-600">{{ productInfo.shipping.first }}元</div>
                <div class="text-sm text-gray-400 mt-1">{{ productInfo.shipping.note }}</div>
              </div>
            </div>
          </div>
          
          <div class="space-y-5">
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">販售期間</span>
              <div class="text-right">
                <div class="text-gray-600">{{ productInfo.saleTime.start }}</div>
                <div class="text-gray-600 mt-1">～{{ productInfo.saleTime.end }}</div>
              </div>
            </div>
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">付款方式</span>
              <div class="text-right">
                <div v-for="method in productInfo.payment" 
                     :key="method" 
                     class="text-gray-600 mb-1">{{ method }}</div>
              </div>
            </div>
            <div class="flex items-center justify-between border-b border-gray-100 pb-3">
              <span class="text-gray-500">預計發售日期</span>
              <span class="font-medium text-gray-600">{{ productInfo.releaseDate }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- 獎項列表 -->
      <div class="bg-white rounded-2xl p-8 mb-8 shadow-sm">
        <h2 class="text-xl font-medium text-gray-700 mb-8">獎項一覽</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="prize in prizes" 
               :key="prize.rank"
               class="border border-gray-100 rounded-xl p-6 hover:shadow-lg transition-shadow duration-300">
            <div class="relative">
              <!-- 獎項等級標籤 -->
              <div class="absolute top-2 left-2 bg-orange-50 text-orange-500 px-4 py-1.5 rounded-full text-sm font-medium">
                {{ prize.rank }}
              </div>
              <!-- 機率標籤 -->
              <div class="absolute top-2 right-2 bg-blue-50 text-blue-500 px-4 py-1.5 rounded-full text-sm">
                機率 {{ prize.probability }}
              </div>
              <!-- 獎品圖片 -->
              <img :src="prize.image" 
                   :alt="prize.name"
                   class="w-full h-52 object-contain my-6">
            </div>
            <h3 class="text-lg font-medium text-gray-700 mb-2">{{ prize.name }}</h3>
            <p class="text-gray-500 text-sm leading-relaxed">{{ prize.description }}</p>
          </div>
        </div>
      </div>

      <!-- 購買區域 -->
      <div class="bg-white rounded-2xl p-6 shadow-sm sticky bottom-4 border border-gray-100">
        <div class="flex items-center justify-between">
          <div class="flex items-center gap-5">
            <button @click="decreaseQuantity"
                    class="w-11 h-11 rounded-full border border-gray-200 flex items-center justify-center text-gray-500 hover:border-orange-300 hover:text-orange-500 transition-colors duration-300">
              -
            </button>
            <span class="text-xl font-medium text-gray-700 min-w-[2ch] text-center">{{ quantity }}</span>
            <button @click="increaseQuantity"
                    class="w-11 h-11 rounded-full border border-gray-200 flex items-center justify-center text-gray-500 hover:border-orange-300 hover:text-orange-500 transition-colors duration-300">
              +
            </button>
          </div>
          <button class="bg-orange-500 hover:bg-orange-400 text-white px-10 py-3 rounded-full font-medium transition-colors duration-300 shadow-sm hover:shadow">
            立即購買
          </button>
        </div>
        <div class="mt-4 text-center text-gray-400 text-sm">
          ※ 單次最多可購買 {{ productInfo.boxCount }} 個
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.prize-image {
  aspect-ratio: 1;
}
</style> 