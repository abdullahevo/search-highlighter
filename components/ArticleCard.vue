<template>
  <article>
    <h2 class="article-title" v-html="highlightMatch(result.title)"></h2>
    <p class="article-content" v-html="highlightMatch(result.content)"></p>
  </article>
</template>

<script lang="ts" setup>
const props = defineProps({
  result: {
    required: true,
    type: Object,
  },
  query: {
    required: true,
    type: String,
  },
});

const highlightMatch = (text: string): string => {
  if (!props.query) return text;
  const regex = new RegExp(`(${props.query})`, "gi");
  return text.replace(regex, "<mark>$1</mark>");
};
</script>

<style></style>
