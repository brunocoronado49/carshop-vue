<template>
  <div>
    <img alt="Store logo" src="./assets/descarga.png" width="150" height="150">
    <br><br>
    <Title title="Store"/>
    <Credits author="José Francisco Rangel Coronado"/>
    <hr/>
    <Content/>
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Credits from './components/Credits.vue'
import Content from './components/Content.vue'

export default {
  name: 'App',
  components: {
    Title,
    Credits,
    Content
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

body {
  background: #f1f2f6;
}

h1, h2, h3, h4, p {
  font-weight: bold;
}
</style>
