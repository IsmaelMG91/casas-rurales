<template>
  <div>
    <div class="grid">
      <article v-for="h in houses" :key="h.id" class="card">
        <div class="row">
          <h2 class="title">
            <NuxtLink class="link" :to="`/houses/${h.id}`">{{
              h.name
            }}</NuxtLink>
          </h2>
          <span class="price">{{ h.price }} € / noche</span>
        </div>
        <p class="desc">{{ h.description }}</p>
        <img :src="config.public.apiBase + h.image"/>
        <div class="row end">
        </div>
      </article>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { House } from '~/types/houses';

const config = useRuntimeConfig();

useSeoMeta({
  title: `${config.public.siteName}`,
  description:
    'A tiny Nuxt 4 rural houses renting demo: SSR data fetching, Nitro API and state.',
});
const { data: houses } = await useFetch<House[]>('/api/houses',{baseURL:config.public.apiBase});
</script>

<style scoped>
.hint {
  color: #6b7280;
  margin: 6px 0 20px;
}
.grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
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
.title {
  font-size: 18px;
}
.link {
  color: #6a6120;
  text-decoration: none;
}
.link:hover {
  text-decoration: underline;
}
.desc {
  margin: 0.8rem 0;
  color: #4b5563;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
.row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}
.row.end {
  margin-top: auto;
  justify-content: flex-end;
}
.price {
  font-weight: 500;
}
.error {
  background: #fff7ed;
  border: 1px solid #fed7aa;
  padding: 12px;
  border-radius: 12px;
}
@media (max-width: 720px) {
  .grid {
    grid-template-columns: 1fr;
  }
}
</style>