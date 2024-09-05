<script setup>
import { defineProps, defineEmits } from 'vue'
defineProps(['data'])
const emit = defineEmits(['addToCart'])
</script>

<template>
  <div class="col-md-4">
    <div class="list-group">
      <a
        v-for="drinks in data"
        :key="drinks.id"
        href="#"
        class="list-group-item list-group-item-action"
        @click="emit('addToCart', drinks)"
      >
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">{{ drinks.name }}</h5>
          <small>{{ drinks.price }}</small>
        </div>
        <p class="mb-1">{{ drinks.description }}</p></a
      >
    </div>
  </div>
</template>
