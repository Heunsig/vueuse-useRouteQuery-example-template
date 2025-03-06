<script setup lang="ts">
import {
  FormControl,
  FormField,
  FormItem,
  FormLabel,
} from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import ProductList from './components/ProductList.vue';
</script>


<template>
  <div class="grid grid-cols-12 gap-4 py-10 mx-auto max-w-7xl">
    <div class="col-span-2">
      <form class="w-full space-y-6">
        <FormField v-slot="{ componentField }" name="username">
          <FormItem>
            <FormLabel>Name</FormLabel>
            <FormControl>
              <Input type="text" placeholder="Product Name" v-bind="componentField" />
            </FormControl>
          </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="username">
          <FormItem>
            <FormLabel>Price</FormLabel>
            <FormControl>
              <Input type="text" placeholder="Product Price" v-bind="componentField" />
            </FormControl>
          </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="username">
          <FormItem>
            <FormLabel>Description</FormLabel>
            <FormControl>
              <Input type="text" placeholder="Description" v-bind="componentField" />
            </FormControl>
          </FormItem>
        </FormField>
      </form>
    </div>
    <div class="col-span-8 col-end-12 ">
      <ProductList />
    </div>
  </div>
</template>
