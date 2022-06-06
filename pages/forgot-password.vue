<template>
  <div class="page page-center">
    <div class="container-tight py-4">
      <div class="text-center mb-4">
        <nuxt-link to="/" class="navbar-brand navbar-brand-autodark">
          <img src="~/assets/logo.svg" height="36" alt="" />
        </nuxt-link>
      </div>
      <form class="card card-md" method="post" @submit.prevent="userRegister">
        <div class="card-body" v-if="message == undefined">
          <h2 class="card-title text-center mb-4">Forgot password</h2>
          <p class="text-muted mb-4">Enter your email address and your password will be reset and emailed to you.</p>
          <div class="alert alert-danger" v-if="errors.error != undefined" role="alert">
            {{ errors.error[0] }}
          </div>
          <div class="mb-3">
            <label class="form-label">Email address</label>
            <input type="email" v-model="form.email" class="form-control" placeholder="Enter email"
              :class="errors.email != undefined ? 'is-invalid' : undefined" />
            <div v-if="errors.email != undefined" class="invalid-feedback">
              <span v-for="message in errors.email" :key="message">{{ message }}</span>
            </div>
          </div>
          <div class="form-footer">
            <button type="submit" class="btn btn-primary w-100">
              <mail-forward-icon />
              Send me new password
            </button>
          </div>
        </div>
        <div class="card-body" v-else>
          <h2 class="card-title text-center mb-4">Forgot password</h2>
          <div class="alert alert-success" v-if="message != undefined" role="alert">
            {{ message }}
          </div>
          <div class="form-footer">
            <nuxt-link to="/login" type="submit" class="btn btn-primary w-100">
              <login-icon />
              Back to Login
            </nuxt-link>
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
        Have account? <nuxt-link to="/login" tabindex="-1">Log In</nuxt-link>
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
      form: {
        email: undefined,
      },
      errors: {
        email: undefined,
        error: undefined,
      },
      message: undefined
    }
  },
  methods: {
    async userRegister(frm) {
      frm.preventDefault();
      try {
        await this.$axios
          .$post("auth/reset-password", {
            email: this.form.email,
          })
          .then(res => {
            console.log(res.message);
            this.message = res.message;
            //this.$router.push('/');
          });
      } catch (e) {
        //console.log(e.response.data.message);
        this.errors = e.response.data.message;
      }


    }
  }
}
</script>
