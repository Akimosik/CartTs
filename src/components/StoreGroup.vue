<template>
  <div class="text-xl font-bold">{{ GroupName }}</div>
  <div v-for="(StoreGood, key) in GroupItems" :key="key">
    <StoreGroupGood
      :StoreGood="StoreGood"
      :isExpensive="isExpensive"
      :ExchangeRate="ExchangeRate"
      @addToCart="addToCart"
    />
  </div>
</template>

<script lang="ts" setup>
import { type Good } from '@/types/Data/Good'
import StoreGroupGood from './StoreGroupGood.vue'
interface Props {
  GroupName: string | number
  GroupItems: Good[]
  ExchangeRate: number
  isExpensive: boolean
}

const addToCart = (StoreGood: Good) => {
  emit('add-to-cart', StoreGood)
}

const emit = defineEmits(['add-to-cart'])
defineProps<Props>()
</script>

<style lang="scss" scoped></style>
