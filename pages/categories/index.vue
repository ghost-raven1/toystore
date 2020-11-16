<template>
  <div>

      <form class="uk-search uk-search-large uk-align-center uk-margin">
          <span uk-search-icon></span>
          <input class="uk-search-input" v-model="query" type="search" placeholder="Поиск товаров...">
      </form>

      <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin" v-for="category in filteredList" v-bind:key="category.id" uk-grid>
          <div class="uk-card-media-left uk-cover-container">
              <img :src="'http://localhost:1337' + category.image.url" alt="" uk-cover>
              <canvas width="600" height="400"></canvas>
          </div>
          <div>
              <div class="uk-card-body">
                  <h3 class="uk-card-title">{{ category.name }}</h3>
                  <p>{{ category.description }}</p>

                  <router-link :to="/categories/ + category.id" tag="a" class="uk-button uk-button-primary">Посмотреть товары
                  </router-link>
              </div>
          </div>
      </div>

      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <img src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
       <p>Категории товаров не найдены!</p>
     </div>

  </div>

</template>

<script>

import categoriesQuery from '~/apollo/queries/category/categories.gql'

export default {
  data() {
    return {
      categories: [],
      query: ''
    }
  },
  apollo: {
    categories: {
      prefetch: true,
      query: categoriesQuery
    }
  },
  computed: {
    // Поисковая система
    filteredList() {
      return this.categories.filter(category => {
        return category.name.toLowerCase().includes(this.query.toLowerCase())
      })
    },
  }
}
</script>