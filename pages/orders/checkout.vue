<template>
<div>

  <a class="uk-button uk-button-primary uk-margin uk-animation-fade uk-transform-origin-bottom-right uk-border-rounded" @click="$router.go(-1)"><span uk-icon="arrow-left"></span> вернуться</a>

  <client-only placeholder="Chargement...">

    <div uk-grid>
        <div class="uk-width-1-3@m">

          <div class="uk-card uk-card-default uk-card-body uk-width-1-1@m">

            <form @submit.stop.prevent="handleSubmit">
                <fieldset class="uk-fieldset">

                    <legend class="uk-legend">Данные покупателя</legend>

                    <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Адрес</label>
                        <input class="uk-input" v-model="address" type="text" placeholder="13 boulevard francis">
                    </div>

                    <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Город</label>
                        <input class="uk-input" v-model="city" type="text" placeholder="San francisco">
                    </div>

                    <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Почтовый код</label>
                        <input class="uk-input" v-model="postalCode" type="text" placeholder="92000">
                    </div>

                    <div class="uk-margin">
                      <label for="card">Данные карты</label>
                        <card
                          ref="card-stripe"
                          stripe="pk_test_51HoQMyJVYMAMD75kimKmu3ydvV6ToPqGP1lM3ExswCS5OtcUMM8rD7NqwI3dasAtS8pwC92GYsy1NrazoDzgyuzF00VSdYVH22"
                          @change='complete = $event.complete'
                        />

                    </div>

                    <div class="uk-margin">
                    <button class="uk-button uk-button-primary uk-animation-fade uk-transform-origin-bottom-right uk-border-rounded" v-if="$route.path !== '/orders/checkout'" @click="goToCheckout" name="button">Оформить заказ ({{ price }}P)</button>
                    </div>

                </fieldset>
            </form>
          </div>

        </div>
        <div class="uk-width-expand@m">
            <Cart />
        </div>
    </div>
  </client-only>


</div>
</template>

<script>
import Cart from '~/components/Cart.vue'
import { Card, createToken } from 'vue-stripe-elements-plus'
import strapi from '~/utils/Strapi'

export default {
  components: {
    Card,
    Cart
  },
  data() {
    return {
      address: '',
      postalCode: '',
      city: '',
      complete: false,
      loading: false
    }
  },
  methods: {
    async handleSubmit() {
      this.loading = true
      let token
      try {
        const response = await createToken()
        token = response.token.id
      } catch (err) {
        alert('An error occurred.')
        this.loading = false
        return
      }
      try {
        await strapi.createEntry('orders', {
          amount: this.$store.getters['cart/price'],
          products: this.$store.getters['cart/items'],
          address: this.address,
          postalCode: this.postalCode,
          city: this.city,
          token
        })
        alert('Ваш заказ успешно оформлен.')
        this.emptyCart()
        this.$router.push('/')
      } catch (err) {
        this.loading = false
        alert('An error occurred.')
      }
    }
  }
}
</script>