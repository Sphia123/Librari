<template>
  <div v-if="book">
    <button class="back-button" @click="goBack">← Назад в каталог</button>

    <h1>{{ book.title }}</h1>
    <img :src="imageSrc" :alt="book.title" />
    <p>{{ book.description }}</p>
  </div>
</template>


<script>
import books from '@/books.js'

export default {
  props: ['id'],
  data() {
    return {
      book: null,
      imageSrc: ''
    }
  },
  created() {
    this.book = books.find(b => b.id === Number(this.id))
    if (this.book) {
      this.imageSrc = new URL(`../assets/${this.book.image}`, import.meta.url).href
    }
  },
  methods: {
    goBack() {
      this.$router.push('/Catalog.vue')  // если у тебя каталог по другому пути, поменяй '/catalog' на нужный
    }
  }
}
</script>

<style scoped>
.back-button {
  background: none;
  border: none;
  color: #2d89ef;
  font-size: 1rem;
  cursor: pointer;
  margin-bottom: 1rem;
  padding: 0;
  transition: color 0.2s ease;
}

.back-button:hover {
  color: #1b5dbf;
}

</style>
