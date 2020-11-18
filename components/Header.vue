<template>
  <client-only>
  <nav class="uk-navbar-container" uk-navbar>
      <div class="uk-navbar-left">

          <ul class="uk-navbar-nav">
              <li class="uk-active"><router-link tag="a" class="navbar-brand" to="/" exact>Toystore</router-link></li>
              <li><router-link tag="a" class="navbar-brand" to="/categories" exact>Товары</router-link></li>
              <li><router-link tag="a" class="navbar-brand" to="/themes" exact>Блог</router-link></li>
          </ul>

      </div>

      <div class="uk-navbar-right">

          <ul class="uk-navbar-nav" v-if="username">
              <li><a class="uk-link-reset"><img src="https://кенгуру-пицца.рф/assets/theme/img/lk.png" class="uk-border-circle" height="40" width="40" alt="">{{ username }}</a></li>
              <li><a @click="logout">Выйти</a></li>
          </ul>

          <ul class="uk-navbar-nav" v-else>
              <li><a href="/users/register">Зарегистрироваться</a></li>
              <li><a href="/users/signin">Войти</a></li>
          </ul>

      </div>

  </nav>
</client-only>

</template>

<script>
import { mapMutations } from 'vuex'

export default {
  computed: {
    // Set your username thanks to your getter
    username() {
      return this.$store.getters['auth/username']
    }
  },
  methods: {
    // Define your needed mutations, here: auth/logout
    ...mapMutations({
      logout: 'auth/logout'
    })
  }
}
</script>