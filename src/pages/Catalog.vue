<template>
  <div class="catalog-page">
    <div class="catalog-header">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Поиск по названию..."
        class="search-input"
      />
      <h2 class="catalog-title">КАТАЛОГ</h2>
      <button class="home-button" @click="goHome">ВЕРНУТЬСЯ НА ГЛАВНУЮ</button>
    </div>

    <div class="catalog">
      <router-link
        v-for="book in filteredBooks"
        :key="book.id"
        :to="`/details/${book.id}`"
        class="book-card"
      >
        <img :src="book.image" :alt="book.title" />
        <h3>{{ book.title }}</h3>
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import initialBooks from '../data/books.js'

const router = useRouter()
const books = ref([...initialBooks])
const searchQuery = ref('')

const filteredBooks = computed(() =>
  books.value.filter(book =>
    book.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
)

const goHome = () => {
  router.push('/')
}
</script>

<style scoped>
html, body {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
}

#app, .catalog-page {
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
}

.catalog-page {
  height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 20px;
  box-sizing: border-box;
  margin: 0;
}

.catalog-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.catalog {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 20px;
  overflow-y: auto;
  height: calc(100vh - 20px*2 - 56px - 24px);
  box-sizing: border-box;
  margin: 4px;
  padding: 0;
  width: 100%;
}



.search-input {
  flex: 1;
  max-width: 400px;
  padding: 0.6rem 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 1rem;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.catalog-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
  white-space: nowrap;
  margin-left: auto;
}

.home-button {
  padding: 0.5rem 1rem;
  background-color: #4a90e2;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  white-space: nowrap;
  transition: background-color 0.2s ease;
}
.home-button:hover {
  background-color: #357ab8;
}

.book-card {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  overflow: hidden;
  text-align: center;
  cursor: pointer;
  text-decoration: none;
  color: inherit;
  transition: transform 0.2s ease;
}

.book-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 15px rgba(0,0,0,0.15);
}

.book-card img {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.book-card h3 {
  margin: 0.5rem 0;
  font-size: 1.1rem;
  color: #333;
  line-height: 100%;
}

.book-card p {
  font-size: 0.9rem;
  color: #000;
  padding: 0 0.5rem 1rem;
}

@media (max-width: 1000px) {
  .catalog {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 600px) {
  .catalog {
    grid-template-columns: 1fr;
  }

  .catalog-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }

  .catalog-title {
    margin-left: 0;
  }

  .home-button {
    align-self: flex-start;
  }
}
</style>
