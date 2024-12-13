<script setup lang="ts">
import type { TBook } from "@/types";
import { computed } from "vue";

const props = defineProps<{
  books: TBook[];
}>();

const emit = defineEmits<{
  (e: "book-selected", book: TBook): void;
}>();

const sortedBooks = computed(() =>
  props.books.sort((a, b) => {
    return a.title.localeCompare(b.title);
  })
);

const selectBook = (book: TBook) => {
  emit("book-selected", book);
};
</script>

<template>
  <aside>
    <div v-for="book in sortedBooks" :key="book.title">
      <button @click="selectBook(book)">
        <span>{{ book.title }}</span>
      </button>
    </div>
  </aside>
</template>

<style>
aside {
  max-width: 600px;
  background-color: #bcbcbc;
}

aside button {
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
  display: block;
  width: 100%;
}
</style>
