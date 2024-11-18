<template>
  <div class="container">
    <h1>Articles</h1>
    <div class="row">
      <div
        v-for="article in paginatedArticles"
        :key="article.id"
        class="col-md-6 mb-4"
      >
        <div class="card">
          <img
            :src="article.imgUrl"
            class="card-img-top"
            :alt="article.title"
          />
          <div class="card-body">
            <h5 class="card-title">{{ article.title }}</h5>
            <a
              :href="`/articles/${encodeURIComponent(
                article.title.toLowerCase().replace(/ /g, '-')
              )}`"
              class="btn btn-primary"
            >
              Read More
            </a>
          </div>
        </div>
      </div>
    </div>
    <!-- Pagination -->
    <nav aria-label="Page navigation" class="mt-4">
      <ul class="pagination">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a class="page-link" @click.prevent="goToPage(currentPage - 1)">
            Previous
          </a>
        </li>
        <li
          v-for="page in totalPages"
          :key="page"
          class="page-item"
          :class="{ active: page === currentPage }"
        >
          <a class="page-link" @click.prevent="goToPage(page)">
            {{ page }}
          </a>
        </li>
        <li class="page-item" :class="{ disabled: currentPage === totalPages }">
          <a class="page-link" @click.prevent="goToPage(currentPage + 1)">
            Next
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const articles = ref([
  { id: 1, title: 'Article 1', imgUrl: 'https://via.placeholder.com/150' },
  { id: 2, title: 'Article 2', imgUrl: 'https://via.placeholder.com/150' },
  { id: 3, title: 'Article 3', imgUrl: 'https://via.placeholder.com/150' },
  { id: 4, title: 'Article 4', imgUrl: 'https://via.placeholder.com/150' },
  { id: 5, title: 'Article 5', imgUrl: 'https://via.placeholder.com/150' },
  { id: 6, title: 'Article 6', imgUrl: 'https://via.placeholder.com/150' },
]);

const currentPage = ref(parseInt(route.params.page || 1));
const articlesPerPage = 4;

const paginatedArticles = ref([]);
const totalPages = ref(0);

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    router.push(`/articles/${page}`);
  }
};

onMounted(() => {
  totalPages.value = Math.ceil(articles.value.length / articlesPerPage);
  const startIndex = (currentPage.value - 1) * articlesPerPage;
  paginatedArticles.value = articles.value.slice(
    startIndex,
    startIndex + articlesPerPage
  );
});
</script>
