<script setup lang="ts">
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
import { Input } from '@/components/ui/input'
import { products } from '@/mock/products'

const categories = ["All", ...new Set(products.map(product => product.category))]

</script>
<template>
  <div class="w-full space-y-6">
    <div>
      <label>Category</label>
      <Select >
        <SelectTrigger>
          <SelectValue placeholder="Select Category" />
        </SelectTrigger>
        <SelectContent>
          <SelectGroup>
            <SelectItem v-for="category in categories" :key="category" :value="category">
              {{ category }}
            </SelectItem>
          </SelectGroup>
        </SelectContent>
      </Select>
    </div>
    <div>
      <label>Name</label>
      <Input type="text" placeholder="Product Name"/>
    </div>

    <div>
      <label>Price</label>
      <div class="flex gap-2">
        <Input type="number" placeholder="Min Price" />
        <Input type="number" placeholder="Max Price" />
      </div>
    </div>
    <div>
      <label>Description</label>
      <Input type="text" placeholder="Description" />
    </div>
  </div>
</template>