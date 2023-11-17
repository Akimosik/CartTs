<template>
  <h1 class="text-3xl font-bold">Магазин</h1>
  <!-- </div> -->
  <p v-for="(Group, key) in sortedarray" :key="key" class="pt-6 md:p-8">
    <StoreGroup
      :GroupItems="Group"
      :GroupName="key"
      :isExpensive="isExpensive"
      :ExchangeRate="ExchangeRate"
      @addToCart="addToCart"
    />
  </p>
  <h1 class="text-3xl font-bold">Корзина</h1>

  <!-- <p v-for="(Group, key) in Cart" :key="key" class="pt-6 md:p-8"> -->
  <StoreCart
    :Cart="Cart"
    :ExchangeRate="ExchangeRate"
    :isExpensive="isExpensive"
    @removeFromCart="removeFromCart"
    @updateQuantity="updateQuantity"
  />
  <!-- </p> -->
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import StoreCart from './components/StoreCart.vue'
import StoreGroup from './components/StoreGroup.vue'
import Mygoods from './json/data.json'
import MyNames from './json/names.json'
import type { Good } from './types/Data/Good'
import type { RootGoods } from './types/Data/RootGoods'
import type { SortedData } from './types/Data/SortedData'
import type { RootNames } from './types/Names/RootNames'

let items: RootGoods = Mygoods
let names: RootNames = MyNames
let isExpensive = ref(false)

const random = (min: number, max: number): number => Math.floor(Math.random() * (max - min)) + min

let ExchangeRate = ref(random(20, 80))

watch(ExchangeRate, (newObj, oldObj) => {
  if (newObj > oldObj) {
    isExpensive.value = true
  } else {
    isExpensive.value = false
  }
})

items.Value.Goods.forEach((el: Good) => {
  el.GroupName = names[el.G as keyof typeof names].G
  el.Name = names[el.G as keyof typeof names].B[el.T].N
  el.CartQuantity = 0
})

const formatData = (data: Good[]) =>
  data.reduce((acc: SortedData, { GroupName, ...rest }) => {
    if (GroupName !== null && GroupName !== undefined) {
      acc[GroupName] ??= []
      acc[GroupName].push(rest)
    }
    return acc
  }, {})

setInterval(() => {
  ExchangeRate.value = random(20, 80)
}, 5000)

let sortedarray = ref<SortedData>(formatData(items.Value.Goods))

let Cart = ref<Good[]>([])

const addToCart = (Good: Good) => {
  if (Cart.value.find((el) => el.T === Good.T)) {
    if (Good.CartQuantity !== undefined) {
      Good.CartQuantity++
    }
  } else {
    Cart.value.push(Good)
    Good.CartQuantity = 1
  }
}

const removeFromCart = (Good: Good) => {
  Good.CartQuantity = 0
  Cart.value = Cart.value.filter((element) => {
    return element !== Good
  })
  // Cart.value.push(Good)
}

const updateQuantity = (Good: Good, quantity: number) => {
  Good.CartQuantity = quantity
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
</style>
./types/Data/Good
