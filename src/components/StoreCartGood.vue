<template>
  <div :class="isExpensive ? 'bg-red-300' : 'bg-green-300'">
    <p>Наименование :{{ StoreGood.Name }}</p>
    <p>Количество в корзине :{{ StoreGood.CartQuantity }}</p>
    <p>Цена :{{ StoreGood.C * ExchangeRate }}</p>
    <p v-show="StoreGood.P < 3" class="bg-yellow-300">Количество ограничено!</p>
    <button
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
      @click="removeFromCart(StoreGood)"
    >
      Удалить из корзины
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
defineProps<Props>()

const removeFromCart = (StoreGood: Good) => {
  emit('remove-from-cart', StoreGood)
}

const emit = defineEmits(['remove-from-cart'])
</script>

<style lang="scss" scoped></style>
