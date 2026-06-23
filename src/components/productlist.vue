<template>
  <div>
    <ProductItem
      v-for="p in products"
      :key="p.id"
      :product="p"
      @delete="$emit('delete-product', $event)"
      @update-stock="$emit('update-stock', $event)"
    />
  </div>
</template>

<script setup>
import ProductItem from "./ProductItem.vue";

defineProps(["products"]);
</script>