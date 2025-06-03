<template>
  <div class="details-wrapper">
    <div class="details-container" v-if="book">
      <div class="left-panel">
        <img :src="book.image" :alt="book.title" class="cover" />
        <h3 class="genre">{{ book.genre }}</h3>
      </div>

      <div class="right-panel">
        <h1>{{ book.title }}</h1>
        <div class="description-wrapper">
          <p class="description">{{ book.description }}</p>
        </div>

        <!-- Кнопка перехода в каталог -->
        <button class="catalog-button" @click="goToCatalog">Перейти в каталог</button>
      </div>
    </div>

    <div v-else class="not-found">
      <h2>Книга не найдена</h2>
      <button class="catalog-button" @click="goToCatalog">Перейти в каталог</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import books from '../data/books.js'

const route = useRoute()
const router = useRouter()
const book = ref(null)

onMounted(() => {
  const id = Number(route.params.id)
  book.value = books.find(b => b.id === id)
})

const goToCatalog = () => router.push('/catalog')
</script>

<style scoped>
.details-wrapper {
  position: relative;
  height: 100%;
  width: 100%;
}

/* Стрелочка назад */
.back-arrow {
  position: absolute;
  top: 1rem;
  left: 1rem;
  font-size: 2rem;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 10;
}

/* Контейнер с деталями */
.details-container {
  display: flex;
  gap: 2rem;
  padding: 4rem 2rem 2rem; /* сверху добавим отступ под стрелку */
  background: #f7f7f7;
  height: 100%;
  box-sizing: border-box;
}

.left-panel {
  flex: 0 0 40%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: white;
  border-radius: 10px;
  padding: 1rem;
  max-height: 100%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.left-panel img.cover {
  width: 100%;
  border-radius: 8px;
  margin-bottom: 1rem;
  object-fit: contain;
}

.genre {
  font-weight: 700;
  color: #444;
  font-size: 1.5rem;
}

.right-panel {
  flex: 0 0 60%;
  background: white;
  border-radius: 10px;
  padding: 2rem;
  overflow-y: auto;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
h1{
  color: black;
}
.description {
  font-size: 1.2rem;
  color: black;
  line-height: 1.6;
}

.catalog-button {
  margin-top: 2rem;
  padding: 0.75rem 1.5rem;
  background-color: #4a90e2;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
}

.catalog-button:hover {
  background-color: #357ab8;
}

.not-found {
  padding: 2rem;
}
</style>
