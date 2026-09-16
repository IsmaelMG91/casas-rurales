<template>
  <header>
    {{ items.value.length }}
  </header>
</template>

<script setup lang="ts">
const { totalItems } = useCart();
</script>