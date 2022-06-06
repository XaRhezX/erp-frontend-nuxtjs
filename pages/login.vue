<template>
  <div class="page page-center">
    <div class="container-tight py-4">
      <div class="text-center mb-4">
        <nuxt-link to="/" class="navbar-brand navbar-brand-autodark">
          <img src="~/assets/logo.svg" height="36" alt="" />
        </nuxt-link>
      </div>
      <form class="card card-md" method="post" @submit.prevent="userLogin">
        <div class="card-body">
          <h2 class="card-title text-center mb-4">Login to your account</h2>
          <div class="alert alert-danger" v-if="errors.error != undefined" role="alert">
            {{ errors.error[0] }}
          </div>
          <div class="mb-3">
            <label class="form-label">Email address</label>
            <input type="email" v-model="login.email" class="form-control" placeholder="Enter email"
              :class="errors.email != undefined ? 'is-invalid' : undefined" />
            <div v-if="errors.email != undefined" class="invalid-feedback">
              <span v-for="message in errors.email" :key="message">{{ message }}</span>
            </div>
          </div>
          <div class="mb-2">
            <label class="form-label">
              Password
              <span class="form-label-description">
                <nuxt-link to="/forgot-password">I forgot password</nuxt-link>
              </span>
            </label>
            <div class="mb-3">
              <input type="password" v-model="login.password" class="form-control" placeholder="Password"
                :class="errors.password != undefined ? 'is-invalid' : ''" />
              <div class="invalid-feedback" v-if="errors.password != undefined">
                <span v-for="message in errors.password" :key="message">{{ message }}</span>
              </div>
            </div>
          </div>
          <div class="mb-2">
            <label class="form-check">
              <input type="checkbox" class="form-check-input" />
              <span class="form-check-label">Remember me on this device</span>
            </label>
          </div>
          <div class="form-footer">
            <button type="submit" class="btn btn-primary w-100">Sign in</button>
          </div>
        </div>
        <div class="hr-text">or</div>
        <div class="card-body">
          <div class="row">
            <div class="col">
              <a href="#" class="btn btn-white w-100">
                <brand-google-icon />
                Login with Google
              </a>
            </div>
            <div class="col">
              <a href="#" class="btn btn-white w-100">
                <brand-facebook-icon />
                Login with Facebook
              </a>
            </div>
          </div>
        </div>
      </form>
      <div class="text-center text-muted mt-3">
        Don't have account yet? <nuxt-link to="/register" tabindex="-1">Sign up</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'guest',
  layout: 'guest',
  data() {
    return {
      login: {
        email: null,
        password: null
      },
      errors: {
        email: undefined,
        password: undefined,
        error: undefined,
      },
    }
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith('local', {
          data: this.login
        })
        this.$router.push('/');

      } catch (e) {
        this.errors = e.response.data.message
      }
    }
  }
}
</script>
