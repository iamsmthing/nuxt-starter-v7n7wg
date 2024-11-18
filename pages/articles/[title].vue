<template>
  <div class="container">
    <h1>{{ article?.title }}</h1>
    <img :src="article?.imgUrl" alt="Article Image" class="img-fluid my-4" />
    <p>{{ article?.details }}</p>
    <router-link to="/articles/1" class="btn btn-primary"
      >Back to Articles</router-link
    >
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const articles = ref([
  {
    id: 1,
    title: 'Article 1',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 1',
  },
  {
    id: 2,
    title: 'Article 2',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 2',
  },
  {
    id: 3,
    title: 'Article 3',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 3',
  },
  {
    id: 4,
    title: 'Article 4',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 4',
  },
  {
    id: 5,
    title: 'Article 5',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 5',
  },
  {
    id: 6,
    title: 'Article 6',
    imgUrl: 'https://via.placeholder.com/150',
    details: 'Details about Article 6',
  },
]);

const article = ref(null);

onMounted(() => {
  const titleSlug = decodeURIComponent(route.params.title);
  article.value = articles.value.find(
    (a) => a.title.toLowerCase().replace(/ /g, '-') === titleSlug
  );
});
</script>
