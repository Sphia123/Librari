<template>
  <router-link :to="`/details/${item.id}`" class="catalog-item">
    <img :src="item.image" alt="cover" />
    <h3>{{ item.title }}</h3>
    <p>{{ item.genre }}</p>
    <p>{{ item.short }}</p>
  </router-link>
</template>

<script setup>
defineProps(['item'])
</script>

<style scoped>
.catalog-item {
  display: block;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  text-decoration: none;
  color: black;
  background: #f9f9f9;
  transition: box-shadow 0.3s;
}

.catalog-item:hover {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.catalog-item img {
  width: 100%;
  height: auto;
  margin-bottom: 1rem;
}
</style>
