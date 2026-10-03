<template>
  <div class="card">
    <h1>{{ house?.name }}</h1>
    <div class="housePresentation">
      <img :src="config.public.apiBase + house?.image"/>
      <div class="houseData">
        <h3>Descripción</h3>
        <p>{{ house?.description }}</p>    
        <h3>Dirección</h3>
        <p>{{ house?.address }}</p>    
        <h3>Habitaciones</h3>
        <p>{{ house?.bedrooms }}</p>
        <h3>Camas</h3>
        <p>{{ house?.beds }}</p>    
        <h3>Baños</h3>
        <p>{{ house?.bathrooms }}</p>
      </div>
    </div>
    <h2>Reviews</h2>
    <div v-for="r in house?.reviews" :key="r.id">
      <p>Fecha: {{ r.date }}</p>
      <p>{{ r.author }}: {{ r.comment }}</p>
      <p>Estrellas: {{ r.rating }}</p>
    </div>
    <!-- <button @click="addToCart()">Add to Cart</button> -->
  </div>
</template>

<script setup lang="ts">
import type { House } from '~/types/houses';

const config = useRuntimeConfig();
const { id } = useRoute().params;
const { addToCart } = useCart();

const {data: house} = await useFetch<House>(`/api/houses/${id}`, {baseURL:config.public.apiBase})

useSeoMeta({
  title: `${house.value?.name}`,
  description: `House ${id} description`
})

</script>

<style scoped>
img {
  height: 20rem;
  object-fit: contain;
}

.card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 14px;
  display: flex;
  flex-direction: column;
  justify-content: start;
}

.housePresentation{
  background-color: aquamarine;
  display: flex;
}

.houseData{
  margin:0.5rem;
  padding: 0 0.5rem;
  display:flex;
  flex-direction: column;
  gap: 0.5rem;
}
</style>