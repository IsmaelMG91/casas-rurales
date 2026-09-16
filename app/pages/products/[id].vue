<template>
  <div>
    <h1>Product</h1>
  </div>
</template>

<script setup lang="ts">
const { id } = useRoute().params;

const { addToCart } = useCart();
</script>