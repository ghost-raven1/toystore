<template>
  <client-only>
  <nav class="uk-navbar-container" uk-sticky="top: 100" uk-navbar>
      <div class="uk-navbar-left">

<button class="uk-button uk-button-default uk-margin-small-right uk-margin-small-left uk-border-rounded uk-visible@s" type="button" 
        uk-toggle="target: #offcanvas-slide"><span uk-icon="icon: menu"></span> Меню</button>

        <div id="offcanvas-slide" uk-offcanvas="overlay: true">
    <div class="uk-offcanvas-bar">
        <button class="uk-offcanvas-close" type="button" uk-close></button>

        <ul class="uk-nav uk-nav-default">
            <li class="uk-nav-header">Меню</li>
            <li><a href="/"><span class="uk-margin-small-right" uk-icon="icon: home"></span> Главная</a></li>
            <li><a href="/categories"><span class="uk-margin-small-right" uk-icon="icon: thumbnails"></span> Товары</a></li>
            <li><a href="/themes"><span class="uk-margin-small-right" uk-icon="icon: table"></span> Блог</a></li>

            <li class="uk-nav-divider"></li>

          <ul class="uk-nav uk-nav-default" v-if="username">
              <li><a class="uk-link-reset"><img src="https://кенгуру-пицца.рф/assets/theme/img/lk.png" class="uk-border-circle" height="40" width="40" alt="">{{ username }}</a></li>
              <li><a class="" @click="logout">Выйти</a></li>
          </ul>

          <ul class="uk-nav uk-nav-default" v-else>
              <li><a class="" href="/users/register"><span class="uk-margin-small-right" uk-icon="icon: user"></span> Зарегистрироваться</a></li>
              <li><a class="" href="/users/signin"><span class="uk-margin-small-right" uk-icon="icon: sign-in"></span> Войти</a></li>
          </ul>

        </ul>

    </div>
</div>

          <ul class="uk-navbar-nav">
              <li class="uk-active"><router-link tag="a" class="navbar-brand" to="/" exact>Toystore</router-link></li>
          </ul>

          <SocialBtns />

      </div>
  </nav>
</client-only>

</template>

<script>
import { mapMutations } from 'vuex'
import SocialBtns from '~/components/btn/Social.vue'

export default {
  components: {
    SocialBtns
  },
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