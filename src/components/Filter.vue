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
import { useRouteQuery } from '@vueuse/router';
import { products } from '@/mock/products'

const categories = ["All", ...new Set(products.map(product => product.category))]

const category = useRouteQuery('category', 'All', { transform: String } )
const name = useRouteQuery('name', '')
const minPrice = useRouteQuery('minPrice', null, { transform: Number })
const maxPrice = useRouteQuery('maxPrice', null, { transform: Number })
const description = useRouteQuery('description', '')

</script>
<template>
  <div class="w-full space-y-6">
    <div>
      <label>Category</label>
      <Select v-model="category">
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
      <Input type="text" placeholder="Product Name" v-model="name"/>
    </div>

    <div>
      <label>Price</label>
      <div class="flex gap-2">
        <Input type="number" placeholder="Min Price" v-model="minPrice"/>
        <Input type="number" placeholder="Max Price" v-model="maxPrice"/>
      </div>
    </div>
    <div>
      <label>Description</label>
      <Input type="text" placeholder="Description" v-model="description"/>
    </div>
  </div>
</template>