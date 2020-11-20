<template>
  <div>

<h1>Добро пожаловать на сайт "Toystore"!</h1>
<ul uk-accordion="multiple: true">
    <li class="uk-open">
        <a class="uk-accordion-title"><h3>Категории товаров</h3></a>
        <div class="uk-accordion-content">

      <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin uk-card-hover uk-border-rounded" v-for="category in categories" v-bind:key="category.id" uk-grid>
          <div class="uk-card-media-left uk-cover-container">
              <img uk-scrollspy="cls:uk-animation-fade" class="uk-border-rounded" :src="'http://localhost:1337' + category.image.url" alt="" uk-cover>
              <canvas width="600" height="400"></canvas>
          </div>
          <div>
              <div class="uk-card-body">
                  <h3 class="uk-card-title">{{ category.name }}</h3>
                  <p>{{ category.description }}</p>

                  <router-link :to="/categories/ + category.id" tag="a" class="uk-button uk-button-primary uk-border-rounded">Посмотреть товары
                  </router-link>
              </div>
          </div>
      </div>

        </div>
    </li>
    <li class="uk-open">
        <a class="uk-accordion-title"><h3>Темы блога</h3></a>
        <div class="uk-accordion-content">
            
            <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin uk-card-hover uk-border-rounded" v-for="theme in themes" v-bind:key="theme.id" uk-grid>
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

        </div>
    </li>
</ul>
<ToTopBtn />
  </div>




</template>

<script>

import categoriesQuery from '~/apollo/queries/category/categories.gql'
import themesQuery from '~/apollo/queries/theme/themes.gql'
import ToTopBtn from '~/components/btn/ToTop.vue'

export default {
  data() {
    return {
      categories: [],
      themes: [],
      query: '',
    }
  },
  components: {
    ToTopBtn,
  },
  apollo: {
    categories: {
      prefetch: true,
      query: categoriesQuery,
    },
    themes: {
      prefetch: true,
      query: themesQuery
    }
  },
}
</script>