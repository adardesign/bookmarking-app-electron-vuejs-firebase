<template>
  <div id="cat-modal" class="ui small modal">
    <i class="close icon"></i>
    <div class="header">
      Add a new Category
    </div>
    <div class="content">
      <form class="ui form">
        <div class="field">
          <label>Category name</label>
          <input type="text" v-model="catName" placeholder="Enter a category name here...">
        </div>
        <div class="field">
          <label>Category Color</label>
          <select v-model="catColor" class="ui simple dropdown">
            <option value="">Select a color</option>
            <option v-for="color in categoryColors">
              {{color}}
            </option>
          </select>
        </div>
      </form>
    </div>
    <div class="actions">
      <div @click="addCategory" class="ui purple inverted button">Save</div>
    </div>
  </div>
</template>

<script>
  import store from '../store';

  export default {
    data () {
      return {
        catName: '',
        catColor: '',
        categoryColors: ['red', 'orange', 'yellow', 'olive', 'green',
          'teal', 'blue', 'violet', 'purple', 'pink', 'brown', 'grey', 'black']
      }
    },

    methods: {
      addCategory() {
        var newCategory = {};
        newCategory[this.catName] = this.catColor;
        store.addCategory(newCategory);
        $('#cat-modal').modal('hide')
      }
    },

    created () {
      const me = this;
      store.on('add-category', () => {
        me.catName = me.catColor = '';
        console.log($('#cat-modal'));
        $('#cat-modal').modal('refresh');

        $('#cat-modal').modal('show');

      });
    }
  }
</script>
