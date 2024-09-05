<script setup>
import { ref, computed } from 'vue'
import MenuList from '@/components/MenuList.vue'
import CartList from '@/components/CartList.vue'
import TheBill from '@/components/TheBill.vue'
const data = [
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60
  }
]
const cart = ref([])
const billing = ref({})
const description = ref('')
const sum = computed(() => cart.value.reduce((pre, next) => pre + next.price * next.quantity, 0))

const addToCart = (drinks) => {
  const clickedItem = cart.value.find((item) => item.id === drinks.id)
  if (clickedItem) {
    clickedItem.quantity += 1
  } else {
    cart.value.push({
      id: drinks.id,
      name: drinks.name,
      description: drinks.description,
      price: drinks.price,
      quantity: 1
    })
  }
  billing.value = {}
}

const updateCart = (item) => {
  cart.value = cart.value.map((cartItem) => {
    if (cartItem.id === item.id) {
      cartItem.quantity = parseInt(item.quantity)
    }
    return cartItem
  })
}

const removeFromCart = (id) => {
  cart.value = cart.value.filter((cartItem) => cartItem.id !== id)
}

const createBilling = () => {
  billing.value = {
    id: new Date().getTime(),
    cart: cart.value,
    description: description.value,
    sum: sum.value
  }
  cart.value = []
  description.value = ''
}
</script>

<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <!-- 選單 -->
        <MenuList :data="data" @add-to-cart="addToCart" />
        <div class="col-md-8">
          <!-- 購物車 -->
          <CartList
            :cartList="cart"
            :sum="sum"
            v-model:description="description"
            @remove-from-Cart="removeFromCart"
            @update-cart="updateCart"
            @create-billing="createBilling"
          />
        </div>
      </div>
      <hr />
      <!-- 結帳單 -->
      <div class="row justify-content-center">
        <div class="col-8">
          <TheBill :bill="billing" />
        </div>
      </div>
    </div>
  </div>
</template>
