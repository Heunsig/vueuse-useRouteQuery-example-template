<template>
  <div>
    <ul class="grid gap-4">
      <li
        v-for="product in products"
        :key="product.id"
        class="p-5 transition-all bg-white border rounded-lg shadow-sm group border-zinc-200 hover:shadow-md dark:border-zinc-800 dark:bg-zinc-950"
      >
        <!-- Product Info -->
        <div class="space-y-3">
          <div class="flex items-center justify-between">
            <h3 class="text-lg font-semibold text-zinc-900 dark:text-zinc-50">
              {{ product.name }}
            </h3>
            <span class="font-medium text-zinc-900 dark:text-zinc-50">
              ${{ formatPrice(product.price) }}
            </span>
          </div>

          <p class="text-sm text-zinc-500 dark:text-zinc-400">
            {{ product.description }}
          </p>

          <div class="flex items-center justify-between">
            <span class="inline-flex items-center rounded-md bg-zinc-100 px-2.5 py-1 text-xs font-medium text-zinc-800 dark:bg-zinc-800 dark:text-zinc-300">
              {{ product.category }}
            </span>
            <div class="space-x-2 text-xs text-zinc-500 dark:text-zinc-400">
              <span>Created: {{ formatDate(product.createdAt) }}</span>
              <span>Updated: {{ formatDate(product.updatedAt) }}</span>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// Props 정의
const props = defineProps({
  initialProducts: {
    type: Array,
    default: () => []
  }
})

// Emits 정의
const emit = defineEmits(['viewDetail', 'addToCart'])

// 상태 관리
const products = ref([
  {
    name: "Wireless Headphones",
    price: 99.99,
    description: "High-quality wireless headphones with noise cancellation.",
    category: "Electronics",
    createdAt: "2025-03-06T12:00:00Z",
    updatedAt: "2025-03-06T12:00:00Z"
  },
  {
    name: "Gaming Mouse",
    price: 49.99,
    description: "Ergonomic gaming mouse with RGB lighting and adjustable DPI.",
    category: "Electronics",
    createdAt: "2025-03-06T12:01:00Z",
    updatedAt: "2025-03-06T12:01:00Z"
  },
  {
    name: "Running Shoes",
    price: 79.99,
    description: "Lightweight and breathable running shoes for all terrains.",
    category: "Footwear",
    createdAt: "2025-03-06T12:02:00Z",
    updatedAt: "2025-03-06T12:02:00Z"
  },
  {
    name: "Smart Watch",
    price: 199.99,
    description: "Feature-rich smartwatch with fitness tracking and heart rate monitor.",
    category: "Electronics",
    createdAt: "2025-03-06T12:03:00Z",
    updatedAt: "2025-03-06T12:03:00Z"
  },
  {
    name: "Laptop Stand",
    price: 34.99,
    description: "Adjustable and ergonomic laptop stand for better posture.",
    category: "Office Supplies",
    createdAt: "2025-03-06T12:04:00Z",
    updatedAt: "2025-03-06T12:04:00Z"
  },
  {
    name: "Bluetooth Speaker",
    price: 59.99,
    description: "Portable Bluetooth speaker with deep bass and long battery life.",
    category: "Electronics",
    createdAt: "2025-03-06T12:05:00Z",
    updatedAt: "2025-03-06T12:05:00Z"
  },
  {
    name: "Desk Lamp",
    price: 25.99,
    description: "Modern LED desk lamp with adjustable brightness settings.",
    category: "Home & Living",
    createdAt: "2025-03-06T12:06:00Z",
    updatedAt: "2025-03-06T12:06:00Z"
  },
  {
    name: "Mechanical Keyboard",
    price: 89.99,
    description: "Mechanical keyboard with customizable RGB backlighting.",
    category: "Electronics",
    createdAt: "2025-03-06T12:07:00Z",
    updatedAt: "2025-03-06T12:07:00Z"
  },
  {
    name: "Fitness Tracker",
    price: 69.99,
    description: "Wearable fitness tracker with step counting and sleep monitoring.",
    category: "Electronics",
    createdAt: "2025-03-06T12:08:00Z",
    updatedAt: "2025-03-06T12:08:00Z"
  },
  {
    name: "Yoga Mat",
    price: 29.99,
    description: "Non-slip yoga mat with extra cushioning for better support.",
    category: "Sports & Outdoors",
    createdAt: "2025-03-06T12:09:00Z",
    updatedAt: "2025-03-06T12:09:00Z"
  },
  {
    name: "Portable Charger",
    price: 39.99,
    description: "Compact power bank with fast charging capabilities.",
    category: "Electronics",
    createdAt: "2025-03-06T12:10:00Z",
    updatedAt: "2025-03-06T12:10:00Z"
  },
  {
    name: "Smartphone Tripod",
    price: 22.99,
    description: "Adjustable tripod stand for smartphones and cameras.",
    category: "Electronics",
    createdAt: "2025-03-06T12:11:00Z",
    updatedAt: "2025-03-06T12:11:00Z"
  },
  {
    name: "Wireless Earbuds",
    price: 79.99,
    description: "True wireless earbuds with noise isolation and long battery life.",
    category: "Electronics",
    createdAt: "2025-03-06T12:12:00Z",
    updatedAt: "2025-03-06T12:12:00Z"
  },
  {
    name: "Water Bottle",
    price: 19.99,
    description: "Insulated stainless steel water bottle that keeps drinks hot or cold.",
    category: "Sports & Outdoors",
    createdAt: "2025-03-06T12:13:00Z",
    updatedAt: "2025-03-06T12:13:00Z"
  },
  {
    name: "Backpack",
    price: 49.99,
    description: "Durable and lightweight backpack with multiple compartments.",
    category: "Travel",
    createdAt: "2025-03-06T12:14:00Z",
    updatedAt: "2025-03-06T12:14:00Z"
  },
  {
    name: "Electric Kettle",
    price: 44.99,
    description: "Fast-boiling electric kettle with auto shut-off.",
    category: "Home & Kitchen",
    createdAt: "2025-03-06T12:15:00Z",
    updatedAt: "2025-03-06T12:15:00Z"
  },
  {
    name: "Coffee Grinder",
    price: 35.99,
    description: "Electric coffee grinder with adjustable settings for fine or coarse grinds.",
    category: "Home & Kitchen",
    createdAt: "2025-03-06T12:16:00Z",
    updatedAt: "2025-03-06T12:16:00Z"
  },
  {
    name: "Sunglasses",
    price: 29.99,
    description: "Polarized sunglasses with UV protection.",
    category: "Fashion",
    createdAt: "2025-03-06T12:17:00Z",
    updatedAt: "2025-03-06T12:17:00Z"
  },
  {
    name: "Portable Fan",
    price: 24.99,
    description: "Rechargeable mini fan with multiple speed settings.",
    category: "Home & Living",
    createdAt: "2025-03-06T12:18:00Z",
    updatedAt: "2025-03-06T12:18:00Z"
  },
  {
    name: "Wireless Charging Pad",
    price: 27.99,
    description: "Fast wireless charging pad compatible with all Qi-enabled devices.",
    category: "Electronics",
    createdAt: "2025-03-06T12:19:00Z",
    updatedAt: "2025-03-06T12:19:00Z"
  }
])

// 유틸리티 함수
const formatDate = (date) => {
  return new Date(date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}

const formatPrice = (price) => {
  return new Intl.NumberFormat('ko-KR').format(price)
}

// 이벤트 핸들러
const handleDetailClick = (productId) => {
  emit('viewDetail', productId)
}

const handleAddToCart = (productId) => {
  emit('addToCart', productId)
}

// 필요한 경우 제품 데이터 fetch
const fetchProducts = async () => {
  try {
    // API 호출 예시
    // const response = await fetch('api/products')
    // products.value = await response.json()
  } catch (error) {
    console.error('제품을 불러오는데 실패했습니다:', error)
  }
}

// 컴포넌트 마운트 시 데이터 로드
onMounted(() => {
  if (products.value.length === 0) {
    fetchProducts()
  }
})
</script>