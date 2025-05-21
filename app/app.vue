<template>
  <div>
    <header>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/news">News</NuxtLink>
    </header>
    <NuxtPage />
  </div>
</template>

<style>
header {
  display: flex;
  justify-content: center;
  gap: 1rem;
  padding: 1rem;
}
</style>
