<template>
  <div class="page">
    <Aside />
    <Header />
    <div class="page-wrapper">
      <nuxt />
    </div>
  </div>
</template>

<script>
import Navbar from '~/components/Navbar'
import Aside from '~/components/Aside.vue'

export default {
  components: {
    Navbar,
    Aside
  }
}
</script>
