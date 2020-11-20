<template>
<div>

  <BackBtn />

  <client-only>
  <div uk-grid>
      <div class="uk-width-1-3@m">

        <div v-for="product in category.products" v-bind:key="product.id" class="uk-margin">
            <div class="uk-card uk-card-default uk-card-hover">
                <div class="uk-card-media-top">
                    <img uk-scrollspy="cls:uk-animation-fade" class="uk-border-rounded" :src="'http://localhost:1337' + product.image.url" alt="" />
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">{{ product.name }} 
                      <span class="uk-badge uk-badge-purple">{{ product.price }}P</span></h3>
                    <p>{{ product.description }}</p>
                    <span class="uk-badge uk-badge-green">Размер: {{product.size}} {{product.size_units}}</span>
                    <span class="uk-badge uk-badge-red">Вес продукта: {{product.weight}} {{product.weight_units}}</span>
                    <span class="uk-badge uk-badge-yellow">Материал: {{product.material}}</span>
                    <span class="uk-badge uk-badge-blue">Цвет: {{product.color}}</span>
                </div>
                <div class="uk-container uk-container-center uk-text-center" v-if="category.products == []">
                    <img class="uk-animation-fade" src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
                    <p>Категории товаров не найдены!</p>
                </div>
                <div class="uk-card-footer">
                  <button class="uk-button uk-button-primary uk-animation-fade uk-transform-origin-bottom-right uk-border-rounded" @click="addToCart(product)">Добавить в корзину</button>
                </div>
            </div>
        </div>

      </div>


      <div class="uk-width-expand@m low-priority">
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