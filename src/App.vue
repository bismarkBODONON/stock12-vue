<template>
  <div class="container">
    <h1>Gestion de Stock</h1>

    <ProductForm @add-product="addProduct" />

    <ProductList
      :products="products"
      @delete-product="deleteProduct"
      @update-stock="updateStock"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import ProductForm from "./components/productForm.vue";
import ProductList from "./components/productlist.vue";

const products = ref([]);

// Charger depuis localStorage
onMounted(() => {
  const data = localStorage.getItem("stock");
  if (data) products.value = JSON.parse(data);
});

// Sauvegarder automatiquement
watch(products, (val) => {
  localStorage.setItem("stock", JSON.stringify(val));
}, { deep: true });

// Ajouter produit
function addProduct(product) {
  products.value.push({
    id: Date.now(),
    ...product,
    stock: Number(product.stock)
  });
}

// Supprimer produit
function deleteProduct(id) {
  products.value = products.value.filter(p => p.id !== id);
}

// Modifier stock
function updateStock({ id, type }) {
  const product = products.value.find(p => p.id === id);
  if (!product) return;

  if (type === "plus") product.stock++;
  if (type === "minus" && product.stock > 0) product.stock--;
}
</script>

<style>
.container {
  max-width: 700px;
  margin: auto;
  font-family: Arial;
}
</style>