<template>
<div>

  <BackBtn />

  <client-only>
  <div uk-grid>

      <div class="uk-width-small-1-2 uk-width-medium-1-4">
        <div v-for="article in theme.articles" v-bind:key="article.id" class="uk-margin uk-card-hover uk-border-rounded">
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img uk-scrollspy="cls:uk-animation-fade" class="uk-border-rounded" :src="'http://localhost:1337' + article.image.url" alt="" />
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">{{ article.name }}</h3>
                      <div class="uk-column-1-3">
                        <h4>
                          Категория: <span class="uk-badge">{{ theme.name }}</span>
                        </h4>
                        <h4>
                          Опубликовано: <span class="uk-badge">{{article.published_at}}</span>
                        </h4>
                      </div>
                    <p>{{ article.description }}</p>
                </div>
                <div class="uk-card-footer">
                  <p>{{article.body}}</p>
                </div>
            </div>
        </div>
      </div>

  </div>

  <ToTopBtn />

  </client-only>

</div>
</template>

<script>
import BackBtn from '~/components/btn/Back.vue'
import ToTopBtn from '~/components/btn/ToTop.vue'
import themeQuery from '~/apollo/queries/theme/theme.gql'

export default {
  data() {
    return {
      theme: Object
    }
  },
  apollo: {
    theme: {
      prefetch: true,
      query: themeQuery,
      variables () {
        return { id: this.$route.params.id }
      }
    }
  },
    components: {
    BackBtn,
    ToTopBtn
  },
}
</script>