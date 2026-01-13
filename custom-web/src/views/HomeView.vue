<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <main class="page">
    <h1>Home</h1>
    <p>欢迎来到示例应用。</p>
    <p>
      <RouterLink to="/game-2048">前往 2048 页面</RouterLink>
    </p>
  </main>
</template>

<style scoped>
.page {
  padding: 2rem;
}

h1 {
  margin-bottom: 0.5rem;
}
</style>
