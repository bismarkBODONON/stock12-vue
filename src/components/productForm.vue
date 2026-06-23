<template>
  <div>
    <input v-model="name" placeholder="Nom produit" />
    <input v-model="stock" type="number" placeholder="Stock" />

    <button @click="submit">Ajouter</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["add-product"]);

const name = ref("");
const stock = ref(0);

function submit() {
  if (!name.value) return;

  emit("add-product", {
    name: name.value,
    stock: stock.value
  });

  name.value = "";
  stock.value = 0;
}
</script>