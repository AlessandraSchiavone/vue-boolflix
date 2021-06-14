<template>
  <div id="app">
    <main>
      <FilmList />
    </main>
  </div>
</template>

<script>
import FilmList from './components/FilmList.vue'

export default {
  name: 'App',
  components: {
    FilmList,
  }
}
</script>

<style lang="scss">
@import './style/general';
</style>
