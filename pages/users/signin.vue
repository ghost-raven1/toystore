<template>
<div>

  <div class="uk-child-width-1-2@m uk-grid">
      <div>
          <div class="uk-card uk-card-default uk-card-small uk-card-body">
            <img src="https://assets-ouch.icons8.com/preview/457/0b338840-2e33-432e-a547-4d3e5acc960c.png" height="500" width="500" class="uk-align-center uk-animation-fade uk-transform-origin-bottom-right" alt="">
          </div>
      </div>
      <div>
          <div class="uk-card uk-card-default uk-card-large uk-card-body">

              <form @submit.stop.prevent="handleSubmit">
                  <fieldset class="uk-fieldset">

                      <legend class="uk-legend">Войти</legend>

                      <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Email</label>
                        <input class="uk-input" v-model="email" type="email" placeholder="paul.bocuse@gmail.com">
                      </div>

                      <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Пароль</label>
                        <input class="uk-input" v-model="password" type="password">
                      </div>

                      <SubmitBtn />

                      <div class="uk-margin">
                        <p>
                          Еще не зарегистрированы?
                          <router-link :to="{ name: 'users-register'}">
                            Зарегистрироваться
                          </router-link>
                        </p>
                      </div>

                  </fieldset>
              </form>

          </div>
      </div>
  </div>

</div>
</template>

<script>
import { mapMutations } from 'vuex'
import strapi from '~/utils/Strapi'
import SubmitBtn from '~/components/btn/Submit.vue'

export default {
  data() {
    return {
      email: '',
      password: '',
      loading: false
    }
  },
    components: {
      SubmitBtn
  },
  methods: {
    async handleSubmit() {
      try {
        this.loading = true
        const response = await strapi.login(
          this.email,
          this.password
        )
        this.loading = false
        this.setUser(response.user)
        this.$router.go(-1)
      } catch (err) {
        this.loading = false
        alert(err.message || 'An error occurred.')
      }
    },
    ...mapMutations({
      setUser: 'auth/setUser'
    })
  }
}
</script>