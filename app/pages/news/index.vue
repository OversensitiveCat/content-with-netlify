<script lang="ts" setup>
const route = useRoute()

function removeTrailingSlash(path: string): string {
  return path.endsWith('/') && path.length > 1 ? path.slice(0, -1) : path
}

const { data: news } = await useAsyncData(removeTrailingSlash(route.path), () => {
  return queryCollection('news')
    .order('date', 'DESC')
    .all()
})
</script>

<template>
  <div class="news-page">
    <ul v-if="news">
      <li
        v-for="item in news"
        :key="item.id"
      >
        <div class="date">
          {{ item.date }}
        </div>
        <h2>
          {{ item.title }}
        </h2>
        <ContentRenderer :value="item" />
        <NuxtLink :to="item.path">
          Read more
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<style scoped>
ul {
  padding: 4rem 2rem;
  display: grid;
  row-gap: 2rem;
}
</style>
