<template>
  <div>
    <input v-model="search" placeholder="Search..." />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      search: '' // Здесь мы определяем переменную search, чтобы избежать предупреждения
    };
  }
};
</script>