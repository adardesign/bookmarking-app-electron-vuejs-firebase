<template>
  <div id="links-container">
    <div id="toolbar">
      <div class="ui inverted icon fluid input">
        <input type="text" v-model="query" placeholder="Filter your links...">
        <i class="search icon"></i>
      </div>
    </div>
    <div class="ui relaxed divided selection list">
      <bookmark v-for="(bookmark, id) in filteredBookmarks"
        :id="id"
        :title="bookmark.title"
        :url="bookmark.url"
        :category="bookmark.category"
        :color="categories[bookmark.category]">
      </bookmark>
    </div>
  </div>
</template>

<script>
  import Bookmark from './Bookmark.vue';
  import {filterByTitle} from '../filters';

  export default {
    data() {
      return {
        query: ''
      }
    },

    props: ['bookmarks', 'categories'],

    components: {
      Bookmark
    },

    computed: {
      filteredBookmarks() {
        return filterByTitle(this.bookmarks, this.query);
      }
    }
  }
</script>
