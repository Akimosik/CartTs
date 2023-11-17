<template>
  <div :class="isExpensive ? 'bg-red-300' : 'bg-white'">
    <p>Наименование :{{ StoreGood.Name }}</p>
    <p>Цена :{{ StoreGood.C * ExchangeRate }}</p>
    <input
      type="number"
      id="inpcartgood"
      v-model.number="localquantity"
      @input="emit('update-quantity', StoreGood, localquantity)"
    />
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
import { onUpdated, ref } from 'vue'
interface Props {
  StoreGood: Good
  ExchangeRate: number
  isExpensive: boolean
}
const props = defineProps<Props>()
// const editCartQuantity = (StoreGood: Good) => {
//   if (StoreGood.CartQuantity){
//     StoreGood.CartQuantity = localquantity
//   }
// }

const removeFromCart = (StoreGood: Good) => {
  emit('remove-from-cart', StoreGood)
}

const emit = defineEmits(['remove-from-cart', 'update-quantity'])

const localquantity = ref<number | undefined>(props.StoreGood.CartQuantity)

onUpdated(() => {
  if (props.StoreGood.CartQuantity !== undefined) {
    localquantity.value = props.StoreGood.CartQuantity
  }
})
</script>

<style lang="scss" scoped></style>
