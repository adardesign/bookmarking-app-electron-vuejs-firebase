<template>
  <div id="app">
    <sidebar
      :categories="categories"
      v-on:category-selected="setSelectedCategory">
    </sidebar>
    <bookmark-list
      :bookmarks="filteredBookmarks"
      :categories="categories">
    </bookmark-list>
</template>

<script>
  import store from './store';
  import Sidebar from './components/Sidebar.vue';
  import BookmarkList from './components/BookmarkList.vue';
  import { filterByCategory } from './filters';

  export default {
    components: {
      Sidebar,
      BookmarkList
    },

    data () {
      return {
        categories: {},
        bookmarks: {},
        selectedCategory: ''
      }
    },

    created () {
      store.on('data-updated', this.updateListings);
      store.on('category-selected', this.setSelectedCategory)
    },

    methods: {
      updateListings(categories, bookmarks) {
        this.categories = categories;
        this.bookmarks = bookmarks;
      },

      setSelectedCategory (category) {
        this.selectedCategory = category;
      }
    },

    computed: {
      filteredBookmarks () {
        return filterByCategory(this.bookmarks, this.selectedCategory);
      }
    }
  }
</script>
