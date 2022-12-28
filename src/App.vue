<template>
  <HomePage />
</template>

<script>
import 'bootstrap/dist/js/bootstrap'
import HomePage from './components/HomePage.vue'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;500;600;700;900&display=swap')
@import "/src/assets/sass/variables/_bootstrap-variables"
@import "/src/assets/sass/general/_basic"
</style>
