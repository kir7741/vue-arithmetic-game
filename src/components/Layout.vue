<template>
  <div class="wrapper">
    <div class="inner-wrapper">
      <!-- <Start/> -->
      <!-- <Restart/> -->
      <Main/>
    </div>
  </div>
</template>

<script>
// Components
import Start from './Start.vue';
import Restart from './Restart.vue';
import Main from './Main.vue';

export default {
  name: 'Layout',
  components: {
    Start,
    Main,
    Restart
  }
}
</script>

<style scoped lang="scss">
@import '../scss/mixin.scss';
.wrapper {
  height: 100vh;
  min-height: 600px;
  background-color: $primaryOrange;
}
.inner-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  height: 100%;
}
</style>



