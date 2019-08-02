<template>
  <div id="app">
    <Layout/>
  </div>
</template>
<script>
import Layout from './components/Layout.vue'

export default {
  name: 'app',
  components: {
    Layout
  }
}
</script>

<style lang="scss">
@import './scss/mixin.scss';
* {
  box-sizing: border-box;
}
body {
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.btn-group {
  text-align: center;
}
.primary-btn {
  padding: 10px 30px;
  width: 100%;
  background-color: $black;
  color: $primaryOrange;
  font-weight: $primaryFontWeight;
  font-size: 20px;
  transition: all 0.5s;
  &:hover {
    background-color: $white;
    color: $black;
  }
}
button {
  border: 0;
  cursor: pointer;
  &:focus {
    outline: none;
  }
}
@media all and (min-width: 768px) {

  .primary-btn {
    width: 350px;
    font-size: 30px;
  }

} 
@media all and (min-width: 1024px) {

  .primary-btn {
    font-size: 36px;
  }

} 
</style>
