<template>
  <div class="wrapper">
    <div class="inner-wrapper">
      <Start/>
    </div>
  </div>
</template>

<script>
// Components
import Start from './Start.vue';

export default {
  name: 'Layout',
  components: {
    Start
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
@media all and (min-width: 767px) {
  .inner-wrapper {
  }
}
</style>



