<template>
<div class="uk-card uk-card-default uk-card-body uk-margin" uk-sticky="offset: 20; bottom: true">
  <img src="https://assets-ouch.icons8.com/preview/125/6414b067-ba59-46ef-8693-4e190aa466c7.png" class="uk-align-center" height="250" width="250" alt="" />

  <div v-if="price > 0">

    <table class="uk-table uk-table-striped uk-table-small uk-table-responsive">
        <thead>
            <tr>
                <th>Название</th>
                <th>Цена за единицу</th>
                <th>Количество</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in selectedProducts" v-bind:key="product.id">
                <td class="uk-width-1-2">{{ product.name }}</td>
                <td class="uk-table-shrink">{{ product.price }}P</td>
                <td class="uk-table-shrink">{{ product.quantity }}</td>
                <td>
                  <a class="uk-margin-left"><span class="uk-badge" @click="addToCart(product)">+</span></a>
                  <a><span class="uk-badge" style="background: #f0506e;" @click="removeFromCart(product)">-</span></a>
                </td>

            </tr>
        </tbody>
    </table>

    <button class="uk-button uk-button-primary" name="button">Оформить заказ ({{ price }}P)</button>
  </div>

</div>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
  methods:{
    ...mapMutations({
      addToCart: 'cart/add',
      removeFromCart: 'cart/remove'
    })
  },
  computed: {
    id() {
      return this.$route.params.id
    },
    selectedProducts() {
      return this.$store.getters['cart/items']
    },
    price() {
      return this.$store.getters['cart/price']
    },
    numberOfItems() {
      return this.$store.getters['cart/numberOfItems']
    }
  }
}
</script>