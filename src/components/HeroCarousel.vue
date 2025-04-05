<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 輪播圖片數據
const carouselImages = [
  { file: 'slide1.jpg', type: 'jpg' },
  { file: 'slide2.jpg', type: 'jpg' },
  { file: 'slide3.png', type: 'png' },
  { file: 'slide4.png', type: 'png' },
  { file: 'slide5.png', type: 'png' },
  { file: 'slide6.jpg', type: 'jpg' },
]

const slides = carouselImages.map((img, index) => ({
  id: index + 1,
  image: `/carousel/${img.file}`,
  title: `活動 ${index + 1}`,
  bgColor: [
    'bg-yellow-100',
    'bg-cyan-100',
    'bg-red-100',
    'bg-orange-100',
    'bg-purple-100'
  ][index],
  borderColor: [
    'border-yellow-400',
    'border-cyan-400',
    'border-red-400',
    'border-orange-400',
    'border-purple-400'
  ][index]
}))

const currentSlide = ref(0)
const isAutoPlaying = ref(true)
let autoPlayTimer = null

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length
}

const goToSlide = (index) => {
  currentSlide.value = index
}

const startAutoPlay = () => {
  if (!autoPlayTimer) {
    autoPlayTimer = setInterval(nextSlide, 5000)
  }
}

const stopAutoPlay = () => {
  if (autoPlayTimer) {
    clearInterval(autoPlayTimer)
    autoPlayTimer = null
  }
}

const handleMouseEnter = () => {
  if (isAutoPlaying.value) {
    stopAutoPlay()
  }
}

const handleMouseLeave = () => {
  if (isAutoPlaying.value) {
    startAutoPlay()
  }
}

onMounted(() => {
  startAutoPlay()
})

onUnmounted(() => {
  stopAutoPlay()
})
</script>

<template>
  <div class="relative w-full overflow-hidden bg-gradient-to-b from-yellow-50/80 to-white"
       @mouseenter="handleMouseEnter"
       @mouseleave="handleMouseLeave">
    <!-- 主標題 -->
    <div class="absolute top-8 left-1/2 -translate-x-1/2 z-10">
      <h2 class="inline-block text-3xl font-medium px-12 py-4 bg-white/95 rounded-full shadow-sm text-gray-700">
        最新活動
      </h2>
    </div>

    <!-- 幻燈片容器 -->
    <div class="w-full h-screen max-h-[700px]">
      <div class="relative w-full h-full">
        <!-- 幻燈片組 -->
        <div class="relative w-full h-full">
          <div v-for="(slide, index) in slides" 
               :key="slide.id"
               class="absolute inset-0 w-full h-full transition-all duration-700"
               :class="[
                 currentSlide === index ? 'opacity-100 z-10 scale-100' : 'opacity-0 z-0 scale-95'
               ]">
            <!-- 主圖片容器 -->
            <div class="w-full h-full flex items-center justify-center bg-gradient-to-b from-gray-50 to-white p-8">
              <img :src="slide.image" 
                   :alt="slide.title"
                   class="max-w-full max-h-full w-auto h-auto object-contain transition-transform duration-500 hover:scale-105">
            </div>
          </div>
        </div>

        <!-- 導航按鈕 -->
        <button @click="prevSlide"
                class="absolute left-6 top-1/2 -translate-y-1/2 bg-white/90 hover:bg-white text-gray-600 p-4 rounded-full shadow-sm transition-all duration-300 z-20 hover:scale-110">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        <button @click="nextSlide"
                class="absolute right-6 top-1/2 -translate-y-1/2 bg-white/90 hover:bg-white text-gray-600 p-4 rounded-full shadow-sm transition-all duration-300 z-20 hover:scale-110">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 5l7 7-7 7" />
          </svg>
        </button>

        <!-- 指示器 -->
        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex justify-center space-x-4 z-20">
          <button v-for="(_, index) in slides"
                  :key="index"
                  @click="goToSlide(index)"
                  :class="[
                    'w-2.5 h-2.5 rounded-full transition-all duration-300 transform',
                    currentSlide === index 
                      ? 'bg-orange-400 scale-125' 
                      : 'bg-gray-300 hover:bg-gray-400 hover:scale-110'
                  ]">
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

