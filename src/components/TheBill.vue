<script setup>
import { defineProps } from 'vue'
defineProps(['bill'])
const totalPrice = (item) => {
  return item.price * item.quantity
}
</script>

<template>
  <div v-if="!bill.id" class="alert alert-secondary text-center" role="alert">尚未建立訂單</div>
  <div v-else class="card">
    <div class="card-body">
      <div class="card-title">
        <h5>訂單</h5>
        <table class="table">
          <thead>
            <tr>
              <th scope="col">品項</th>
              <th scope="col">數量</th>
              <th scope="col">小計</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in bill.cart" :key="item.id">
              <td>{{ item.name }}</td>
              <td>{{ item.quantity }}</td>
              <td>{{ totalPrice(item) }}</td>
            </tr>
          </tbody>
        </table>
        <div class="text-end">
          備註: <span>{{ bill.description }}</span>
        </div>
        <div class="text-end">
          <h5>
            總計: <span>{{ bill.sum }}</span>
          </h5>
        </div>
      </div>
    </div>
  </div>
</template>
