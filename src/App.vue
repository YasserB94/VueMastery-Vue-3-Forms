<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="w-full">
  <header class="flex justify-between p-4 space-x-60 lg:justify-center">
    <h1>Hello Forms!</h1>
    <nav class="space-x-4">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>
  <main class="mx-2 max-w-xl md:mx-4 lg:mx-auto h-fit w-full">
    <RouterView />
  </main>
  </div>
</template>

<style scoped></style>
