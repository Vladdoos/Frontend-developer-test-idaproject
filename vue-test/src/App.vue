<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
body{
  background: rgba(255, 254, 251, 0.8);
}
#app {
  font-family: 'Source Sans Pro';
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 31px;
  color: #3F3F3F;
}
h1,h2, p{
  color: #3F3F3F;
}
</style>
