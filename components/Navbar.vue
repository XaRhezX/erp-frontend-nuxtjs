<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <nuxt-link class="navbar-brand" to="/">Enterprise Resource Planing</nuxt-link>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto">
          <template v-if="isLoggedIn">
            <li class="nav-item">
              <nuxt-link class="nav-link" to="/user">{{ user.name }} <span class="sr-only">(current)</span></nuxt-link>
            </li>
            <li class="nav-item">
              <a class="nav-link" @click="logout">Logout</a>
            </li>
          </template>
          <template v-else>
            <li class="nav-item">
              <nuxt-link class="nav-link" to="/login">Login</nuxt-link>
            </li>
          </template>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters([
      'user',
      'isLoggedIn'
    ])
  },
  methods: {
    async logout() {
      await this.$auth.logout();
    }
  }
}
</script>
