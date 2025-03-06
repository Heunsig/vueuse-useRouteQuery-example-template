<script setup lang="ts">
import Filter from '@/components/Filter.vue';
import ProductList from '@/components/ProductList.vue';
</script>

<template>
  <div class="grid grid-cols-12 py-10 mx-auto max-w-7xl">
    <div class="col-span-3">
      <Filter class="sticky top-5"/>
    </div>
    <div class="col-span-7 col-end-12 ">
      <ProductList />
    </div>
  </div>
</template>
