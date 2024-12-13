<script setup lang="ts">
import { ref } from "vue";
import AppSidebar from "./components/AppSidebar.vue";
import Content from "./components/Content.vue";
import { books } from "./data";
import type { TBook } from "./types";

const selectedBook = ref<TBook>();

const onBookSelected = (book: TBook) => {
  selectedBook.value = book;
};

const boooks = ref();

const fetchBooks = async () => {
  try {
    const response = await fetch("/get-books");
    const data = response.json();

    boooks.value = data;
  } catch (error) {
    console.error(error);
  }
};

await fetchBooks();
</script>

<template>
  <div :class="$style.container">
    <AppSidebar :books="books" @book-selected="onBookSelected" />

    <div>
      <Content :book="selectedBook" v-if="selectedBook" />
      <p v-if="!selectedBook">Select book</p>
    </div>
  </div>
</template>

<style module>
.container {
  display: flex;
}
</style>
