<template>
<div>

  <BackBtn />

  <client-only>
  <div uk-grid>
      <div class="uk-width-1-3@m">

        <div v-for="product in category.products" v-bind:key="product.id" class="uk-margin">
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img uk-scrollspy="cls:uk-animation-fade" class="uk-border-rounded" :src="'http://localhost:1337' + product.image.url" alt="" />
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">{{ product.name }} <span class="uk-badge">{{ product.price }}P</span></h3>
                    <p>{{ product.description }}</p>
                </div>
                <div class="uk-card-footer">
                  <button class="uk-button uk-button-primary uk-animation-fade uk-transform-origin-bottom-right uk-border-rounded" @click="addToCart(product)">Добавить в корзину</button>
                </div>
            </div>
        </div>

      </div>


      <div class="uk-width-expand@m">
          <Cart />
      </div>
  </div>

  <ToTopBtn />

  </client-only>
</div>
</template>

<script>
import { mapMutations } from 'vuex'
import Cart from '~/components/Cart.vue'
import BackBtn from '~/components/btn/Back.vue'
import ToTopBtn from '~/components/btn/ToTop.vue'
import categoryQuery from '~/apollo/queries/category/category.gql'

export default {
  data() {
    return {
      category: Object
    }
  },
  apollo: {
    category: {
      prefetch: true,
      query: categoryQuery,
      variables () {
        return { id: this.$route.params.id }
      }
    }
  },
  components: {
    Cart,
    BackBtn,
    ToTopBtn
  },
  methods:{
    ...mapMutations({
      addToCart: 'cart/add',
      removeFromCart: 'cart/remove'
    }),
  }
}
</script>