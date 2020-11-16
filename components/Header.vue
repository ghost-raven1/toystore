<template>
  <client-only>
    <nav class="uk-navbar-container" uk-navbar>
        <div class="uk-navbar-left">

            <ul class="uk-navbar-nav">
                <li class="uk-active"><router-link tag="a" class="navbar-brand" to="/" exact>Toystore</router-link></li>
                <li><router-link tag="a" class="navbar-brand" to="/categories" exact>Категории</router-link></li>
            </ul>

        </div>

    </nav>
  </client-only>
</template>