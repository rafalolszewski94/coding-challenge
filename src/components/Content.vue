<script setup lang="ts">
import type { TBook } from "../types";

defineProps<{
  book: TBook;
}>();
</script>

<template>
  <div>
    <h2>{{ book.title }}</h2>
    <small>{{ book.author }}</small>
    <p>{{ book.year }}</p>
    <p>{{ book.genre }}</p>
  </div>
</template>
