<template>
  <div id="app">
    <main>
      <Main />
    </main>
  </div>
</template>

<script>
import Main from './components/Main'

export default {
  name: 'App',
  components: {
    Main,
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import './style/general';
</style>
