<script setup lang="ts">
import {
  FormControl,
  FormField,
  FormItem,
  FormLabel,
} from '@/components/ui/form'
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
import { Input } from '@/components/ui/input'
import ProductList from './components/ProductList.vue';

const categories = [
  "Electronics",
  "Footwear",
  "Office Supplies",
  "Home & Living",
  "Sports & Outdoors",
  "Travel",
  "Home & Kitchen",
  "Fashion"
];
</script>


<template>
  <div class="grid grid-cols-12 py-10 mx-auto max-w-7xl">
    <div class="col-span-3">
      <form class="w-full space-y-6">
        <FormField v-slot="{ componentField }" name="category">
          <FormItem>
            <FormLabel>Category</FormLabel>
            <FormControl>
              <Select>
                <SelectTrigger>
                  <SelectValue placeholder="Select a fruit" />
                </SelectTrigger>
                <SelectContent>
                  <SelectGroup>
                    <SelectItem v-for="category in categories" :key="category" :value="category">
                      {{ category }}
                    </SelectItem>
                  </SelectGroup>
                </SelectContent>
              </Select>
            </FormControl>
          </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="name">
          <FormItem>
            <FormLabel>Name</FormLabel>
            <FormControl>
              <Input type="text" placeholder="Product Name" v-bind="componentField" name="name" />
            </FormControl>
          </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="price">
          <FormItem>
            <FormLabel>Price</FormLabel>
            <FormControl>
              <Input type="number" placeholder="Product Price" v-bind="componentField" name="price" />
            </FormControl>
          </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="description">
          <FormItem>
            <FormLabel>Description</FormLabel>
            <FormControl>
              <Input type="text" placeholder="Description" v-bind="componentField" name="description"/>
            </FormControl>
          </FormItem>
        </FormField>
      </form>
    </div>
    <div class="col-span-7 col-end-12 ">
      <ProductList />
    </div>
  </div>
</template>
