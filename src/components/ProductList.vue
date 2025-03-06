<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { products as mockProducts } from '@/mock/products'

const route = useRoute()

const category = computed(() => route.query.category ?? 'All')
const name = computed(() => route.query.name ?? '')
const minPrice = computed(() => route.query.minPrice ?? null)
const maxPrice = computed(() => route.query.maxPrice ?? null)
const description = computed(() => route.query.description ?? '')

const filteredProducts = computed(() => {
  return mockProducts.filter(product => product.name.toLocaleLowerCase().includes(name.value.toLocaleLowerCase()))
                        .filter(product => minPrice.value ? product.price >= minPrice.value : true)
                        .filter(product => maxPrice.value ? product.price <= maxPrice.value : true)
                        .filter(product => category.value === 'All' ? true : product.category === category.value)
                        .filter(product => description.value ? product.description.toLocaleLowerCase().includes(description.value.toLocaleLowerCase()) : true)
})  

function formatDate(date) {
  return new Date(date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}

function formatPrice(price) {
  return new Intl.NumberFormat('en-US').format(price)
}
</script>

<template>
  <div>
    <ul class="grid gap-4" v-if="filteredProducts.length > 0">
      <li
        v-for="product in filteredProducts"
        :key="product.id"
        class="p-5 transition-all bg-white border rounded-lg shadow-sm group border-zinc-200 hover:shadow-md dark:border-zinc-800 dark:bg-zinc-950"
      >
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
          </div>
        </div>
      </li>
    </ul>
    <div v-else>
      <p class="text-center text-zinc-500 dark:text-zinc-400">
        No products found
      </p>
    </div>
  </div>
</template>

