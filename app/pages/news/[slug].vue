<script lang="ts" setup>
const route = useRoute()

function removeTrailingSlash(path: string): string {
  return path.endsWith('/') && path.length > 1 ? path.slice(0, -1) : path
}

const { data: news } = await useAsyncData(removeTrailingSlash(route.path), () => queryCollection('news').path(route.path).first())

useSeoMeta({
  title: news.value?.title,
  description: news.value?.description,
})
</script>

<template>
  <div class="news-page">
    <main v-if="news">
      <h1>{{ news.name }}</h1>
      <ContentRenderer :value="news" />
    </main>
  </div>
</template>

<style scoped>
main {
  padding: 4rem 2rem;
}
</style>
