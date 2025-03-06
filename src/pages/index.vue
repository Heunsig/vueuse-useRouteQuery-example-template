<script setup lang="ts">
import Filter from '@/components/Filter.vue';
import ProductList from '@/components/ProductList.vue';
import vueuseLogo from '@/assets/vueuse.svg';
</script>

<template>
  <div class="py-10">
    <div class="mx-auto max-w-7xl">
      <h1 class="flex items-center gap-1 text-2xl font-bold">
        <img :src="vueuseLogo" alt="logo" class="w-7 h-7" />
        vueuse `useRouteQuery` Example
      </h1>
    </div>
    <div class="grid grid-cols-12 py-10 mx-auto max-w-7xl">
      <div class="col-span-3">
        <Filter class="sticky top-5"/>
      </div>
      <div class="col-span-7 col-end-12 ">
        <ProductList />
      </div>
    </div>
  </div>
</template>
