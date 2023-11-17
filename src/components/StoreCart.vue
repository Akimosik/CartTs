<template>
  <div v-for="(StoreGood, key) in Cart" :key="key">
    <StoreCartGood
      :StoreGood="StoreGood"
      :ExchangeRate="ExchangeRate"
      :isExpensive="isExpensive"
      @removeFromCart="emit('remove-from-cart', StoreGood)"
    />
  </div>
</template>

<script lang="ts" setup>
import { type Good } from '@/types/Data/Good'
import StoreCartGood from './StoreCartGood.vue'
interface Props {
  ExchangeRate: number
  Cart: Good[]
  isExpensive: boolean
}

const emit = defineEmits(['remove-from-cart', 'update-quantity'])
defineProps<Props>()
</script>

<style lang="scss" scoped></style>
