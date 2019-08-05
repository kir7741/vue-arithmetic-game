<template>
  <div>
    <h3 class="title">
      60 SECONDS CHALLENGE
    </h3>
    <h2 class="score-text">
      <span>—</span>
      <span>
        YOUR FINAL SCORE
      </span>
      <span>—</span>
    </h2>
    <div class="score">
      {{ score }}
    </div>
    <div class="btn-group">
      <button 
        type="button"
        class="primary-btn"
        @click="restartGame"
      >
        TRY AGAIN!
      </button>
    </div>
  </div>
</template>

<script>
// Enums
import FlowStatus from '../enum/flow-status.enum';

export default {
  name: 'Restart',
  props: {
    initScore: Number
  },
  data() {
    return {
      score: this.initScore
    }
  },
  methods: {
    restartGame() {
      this.$emit('restartGame', FlowStatus.PENDING);
    }
  }
}
</script>

<style scoped lang="scss">
@import '../scss/mixin.scss';
.title {
  border: 3px solid $white;
  padding: 5px;
  color: $white;
  text-align: center;
  font-weight: $primaryFontWeight;
}
.score-text {
  text-align: center;
  font-weight: $primaryFontWeight;
  span:first-child,
  span:last-child {
    color: $white;
  }
}
.score {
  margin-bottom: 50px;
  font-size: 80px;
  text-align: center;
  font-weight: $primaryFontWeight;
}
@media all and (min-width: 768px) {
  .title {
    margin-right: auto;
    margin-left: auto;
    max-width: 350px;
  }
  .score-text {
    font-size: 40px;
  }
  .score {
    font-size: 90px;
  }
}
@media all and (min-width: 1024px) {
  .title {
    font-size: 24px;
  }
  .score-text {
    font-size: 56px;
  }
  .score {
    font-size: 110px;
  }
}
</style>