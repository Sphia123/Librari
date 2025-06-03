<template>
  <div class="home-container">
    <!-- Левая часть -->
    <div class="left">
      <h1>Добро пожаловать в Libl </h1>
      <router-link to="/catalog" class="catalog-button">Перейти в каталог</router-link>
    </div>

    <!-- Правая часть: только 2 скролла -->
    <div class="right">
      <div class="scroll-column" v-for="(column, index) in 2" :key="index" :class="{ reverse: index === 1 }">
        <div class="scroll-track">
          <img v-for="book in books" :key="book.id + '-' + index" :src="book.image" :alt="book.title" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import books from '../data/books.js'
</script>

<style scoped>
.home-container {
  display: flex;
  height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 0;
  overflow: hidden;
  box-sizing: border-box;
}

.left {
  flex: 0 0 55%;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 2rem;
  box-sizing: border-box;
}

.left h1 {
  font-size: 3rem;
  color: #333;
  margin: 0;
}

.catalog-button {
  background-color: #42b983;
  color: white;
  padding: 1rem 2rem;
  border-radius: 8px;
  text-decoration: none;
  font-size: 1.2rem;
  transition: background 0.3s;
  width: fit-content;
}

.catalog-button:hover {
  background-color: #369c6c;
}

.right {
  flex: 0 0 45%;
  display: flex;
  gap: 10px;
  overflow: hidden;
  height: 100%;
}

.scroll-column {
  flex: 1;
  overflow: hidden;
  position: relative;
  height: 100%;
}

.scroll-track {
  display: flex;
  flex-direction: column;
  height: 200%;
  animation: scroll 20s linear infinite;
}

.scroll-column.reverse .scroll-track {
  animation-direction: reverse;
}

.scroll-track img {
  width: 100%;
  object-fit: cover;
  height: auto;
}

@keyframes scroll {
  0% {
    transform: translateY(0%);
  }
  100% {
    transform: translateY(-50%);
  }
}

/* Адаптив */
@media (max-width: 900px) {
  .home-container {
    flex-direction: column;
  }

  .left {
    max-width: 100%;
    align-items: center;
    text-align: center;
  }

  .right {
    width: 100vw;
    margin-left: auto;
    gap: 5px;
  }

  .scroll-track img {
    height: 150px;
  }
}

/* Убираем прокрутку всей страницы */
html, body, #app {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  overflow-x: hidden;
  box-sizing: border-box;
}
</style>


