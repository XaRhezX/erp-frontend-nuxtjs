<template>
  <div class="page page-center">
    <div class="container-tight py-4">
      <div class="text-center mb-4">
        <nuxt-link to="/" class="navbar-brand navbar-brand-autodark">
          <img src="~/assets/logo.svg" height="36" alt="" />
        </nuxt-link>
      </div>
      <form class="card card-md" method="post" @submit.prevent="userRegister">
        <div class="card-body">
          <h2 class="card-title text-center mb-4">Create New Account</h2>
          <div class="alert alert-danger" v-if="errors.error != undefined" role="alert">
            {{ errors.error[0] }}
          </div>
          <div class="mb-3">
            <label class="form-label">Full Name</label>
            <input type="text" v-model="register.name" class="form-control" placeholder="Enter email"
              :class="errors.name != undefined ? 'is-invalid' : undefined" />
            <div v-if="errors.name != undefined" class="invalid-feedback">
              <span v-for="message in errors.name" :key="message">{{ message }}</span>
            </div>
          </div>
          <div class="mb-3">
            <label class="form-label">Email address</label>
            <input type="email" v-model="register.email" class="form-control" placeholder="Enter email"
              :class="errors.email != undefined ? 'is-invalid' : undefined" />
            <div v-if="errors.email != undefined" class="invalid-feedback">
              <span v-for="message in errors.email" :key="message">{{ message }}</span>
            </div>
          </div>
          <div class="mb-3">
            <label class="form-label">Password</label>
            <div class="mb-3">
              <input type="password" v-model="register.password" class="form-control" placeholder="Password"
                :class="errors.password != undefined ? 'is-invalid' : ''" />
              <div class="invalid-feedback" v-if="errors.password != undefined">
                <span v-for="message in errors.password" :key="message">{{ message }}</span>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <label class="form-label">Password Confirmation</label>
            <div class="mb-3">
              <input type="password" v-model="register.password_confirmation" class="form-control"
                placeholder="Password" :class="errors.password_confirmation != undefined ? 'is-invalid' : ''" />
              <div class="invalid-feedback" v-if="errors.password_confirmation != undefined">
                <span v-for="message in errors.password_confirmation" :key="message">{{ message }}</span>
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
            <button type="submit" class="btn btn-primary w-100">Sign up</button>
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
      register: {
        name: undefined,
        email: undefined,
        password: undefined,
        password_confirmation: undefined
      },
      errors: {
        name: undefined,
        email: undefined,
        password: undefined,
        password_confirmation: undefined,
        error: undefined,
      },
    }
  },
  methods: {
    async userRegister(frm) {
      frm.preventDefault();
      try {
        await this.$axios
          .$post("auth/register", {
            name: this.register.name,
            email: this.register.email,
            password: this.register.password,
            password_confirmation: this.register.password_confirmation,
          })
          .then(() => {
            this.$router.push('/');
          });
      } catch (e) {
        console.log(e.response.data.message);
        this.errors = e.response.data.message;
      }


    }
  }
}
</script>
