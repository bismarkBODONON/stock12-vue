<template>
  <div class="card">
    <h3>{{ product.name }}</h3>
    <p>Stock: {{ product.stock }}</p>

    <button @click="$emit('update-stock', { id: product.id, type: 'plus' })">+</button>
    <button @click="$emit('update-stock', { id: product.id, type: 'minus' })">-</button>

    <button @click="$emit('delete', product.id)">Supprimer</button>
  </div>
</template>

<script setup>
defineProps(["product"]);
</script>

<style>
.card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
}
</style>