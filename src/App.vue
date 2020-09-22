<template>
  <div id="app">
    <img class="logo" alt="Vue logo" src="./assets/logo.png">
    <h1>Github Repo Fetcher</h1>
    <SearchRepos />
  </div>
</template>

<script>
import SearchRepos from './components/SearchRepos.vue'

export default {
  name: 'App',
  components: {
    SearchRepos
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  width: 150px;
}
</style>
