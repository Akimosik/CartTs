<template>
  <div :class="isExpensive ? 'bg-red-300' : 'bg-white'">
    <p>Наименование :{{ StoreGood.Name }}</p>
    <p>Цена :{{ StoreGood.C * ExchangeRate }}</p>
    <!-- <button @click="AddToCart(StoreGood)">Добавить в корзину</button> -->
    <button
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
      @click="emit('add-to-cart', StoreGood)"
    >
      Добавить в корзину
    </button>
  </div>
</template>

<script lang="ts" setup>
import { type Good } from '@/types/Data/Good'
interface Props {
  StoreGood: Good
  ExchangeRate: number
  isExpensive: boolean
}
const emit = defineEmits(['add-to-cart'])
// const AddToCart = (StoreGood: Good) => {
//   emit('addToCart', StoreGood)
// }

defineProps<Props>()
</script>

<style lang="scss" scoped></style>
