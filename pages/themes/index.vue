<template>
  <div>

      <form class="uk-search uk-search-large uk-align-center uk-margin">
          <span uk-search-icon></span>
          <input class="uk-search-input" v-model="query" type="search" placeholder="Поиск тем блога...">
      </form>

      <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin uk-card-hover uk-border-rounded" v-for="theme in filteredList" v-bind:key="theme.id" uk-grid>
          <div class="uk-card-media-left uk-cover-container">
              <img uk-scrollspy="cls:uk-animation-fade" class="uk-border-rounded" :src="'http://localhost:1337' + theme.image.url" alt="" uk-cover>
              <canvas width="600" height="400"></canvas>
          </div>
          <div>
              <div class="uk-card-body">
                  <h3 class="uk-card-title">{{ theme.name }}</h3>
                  <p>{{ theme.description }}</p>

                  <router-link :to="/themes/ + theme.id" tag="a" class="uk-button uk-button-primary uk-border-rounded">Посмотреть статьи
                  </router-link>
              </div>
          </div>
      </div>

      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <img class="uk-animation-fade uk-transform-origin-bottom-right" src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
       <p>Темы статей не найдены!</p>
     </div>

  </div>

</template>

<script>

import themesQuery from '~/apollo/queries/theme/themes.gql'

export default {
  data() {
    return {
      themes: [],
      query: ''
    }
  },
  apollo: {
    themes: {
      prefetch: true,
      query: themesQuery
    }
  },
  computed: {
    // Поисковая система
    filteredList() {
      return this.themes.filter(theme => {
        return theme.name.toLowerCase().includes(this.query.toLowerCase())
      })
    },
  }
}
</script>