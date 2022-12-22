<template>
  <HomePage />
</template>

<script>
import HomePage from './components/HomePage.vue'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style lang="sass">
@import "assets/sass/variables/_bootstrap-variables"
@import "~bootstrap/scss/bootstrap"
</style>
