<script lang="ts" setup>
const route = useRoute()
const { data: news } = await useAsyncData(route.path, () => queryCollection('news').path(route.path).first())

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
