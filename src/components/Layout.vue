<template>
  <div class="wrapper">
    <div class="inner-wrapper">
      <transition 
        name="fade" 
        mode="out-in"
      >
        <Start
          v-if="flowStep === flowStatus.PENDING"
          @startGame="setFlow"
        />
        <Main
          v-if="flowStep === flowStatus.PLAYING"
          @endGame="setFlow"
          @setScore="setScore"
        />
        <Restart
          v-if="flowStep === flowStatus.END"
          :initScore="score"
          @restartGame="setFlow"
        />
      </transition>
    </div>
  </div>
</template>

<script>
// Components
import Start from './Start.vue';
import Restart from './Restart.vue';
import Main from './Main.vue';

// Enums
import FlowStatus from '../enum/flow-status.enum';

export default {
  name: 'Layout',
  components: {
    Start,
    Main,
    Restart
  },
  data() {
    return {
      flowStatus: FlowStatus, // 遊戲狀態的列舉
      flowStep: FlowStatus.PENDING, // 當前遊戲狀態
      score: 0 // 玩家得分
    }
  },
  methods: {
    /**
     * 設定遊戲狀態
     */
    setFlow(flowStatus) {
      this.flowStep = flowStatus;
    },
    /**
     * 設定分數
     */
    setScore(score) {
      this.score = score;
    }
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
.fade-leave-active {
  transition: opacity 0.5s ease-out;
}
.fade-enter-active {
  transition: opacity 0.5s ease-in;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>



