<template>
  <div class="search-component">
    <!-- Title -->
    <h1 class="title">Article Search</h1>

    <!-- Search Box -->
    <input
      type="text"
      v-model="query"
      @input="search"
      placeholder="Type keywords to search..."
      class="search-input"
    />

    <!-- Search Results -->
    <ul class="results-list">
      <li
        v-for="(result, index) in filteredResults"
        :key="index"
        class="result-item"
      >
      <ArticleCard :result="result" :query="query"/>
      </li>
    </ul>
  </div>
</template>


<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import { ArticleCard } from './.nuxt/components';

interface Article {
  title: string;
  content: string;
}

export default defineComponent({
  name: "SearchHighlight",
  setup() {
    const query = ref<string>(""); // The user's search query

    const articles = ref<Article[]>([
      { title: "Vue.js Basics", content: "Learn the basics of Vue.js, a progressive framework for building UI." },
      { title: "Vue 3 Composition API", content: "A deep dive into Vue 3's Composition API for better code organization." },
      { title: "JavaScript Fundamentals", content: "Understand the building blocks of JavaScript programming." },
      { title: "Styling in Vue", content: "How to use scoped CSS and libraries like Tailwind in Vue applications." },
      { title: "State Management", content: "Explore state management tools like Vuex and Pinia for Vue.js." },
      { title: "Routing with Vue Router", content: "Learn how to set up dynamic routing in your Vue applications." },
      { title: "Building Responsive Apps", content: "Techniques to make your apps look great on all screen sizes." },
      { title: "Testing Vue Apps", content: "Use tools like Jest and Cypress to test your Vue applications." },
      { title: "Deploying Vue Projects", content: "Tips for deploying Vue apps to platforms like Netlify and Vercel." },
      { title: "Best Practices in Vue", content: "Follow these best practices to write clean and maintainable Vue code." },
    ]);

    const filteredResults = computed(() =>
      articles.value.filter(
        (article) =>
          article.title.toLowerCase().includes(query.value.toLowerCase()) ||
          article.content.toLowerCase().includes(query.value.toLowerCase())
      )
    );



    return {
      query,
      filteredResults,
    };
  },
});
</script>


<style scoped>
.search-component {
  max-width: 800px;
  margin: 2rem auto;
  padding: 1rem;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  color: #333;
}

.search-input {
  width: 100%;
  padding: 12px 16px;
  margin-bottom: 1.5rem;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: border 0.3s;
}

.search-input:focus {
  border-color: #007bff;
  outline: none;
}

.results-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.result-item {
  padding: 1rem;
  margin-bottom: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  transition: box-shadow 0.3s;
}

.result-item:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.article-title {
  font-size: 1.25rem;
  margin: 0 0 0.5rem;
  color: #007bff;
}

.article-content {
  font-size: 1rem;
  color: #555;
  margin: 0;
  line-height: 1.6;
}

mark {
  background-color: #ffeeba;
  padding: 0 2px;
  border-radius: 2px;
}
</style>


