<template>
  <div class="box">

    <!-- 遊戲資訊區域開始 -->
    <div>

      <!-- 分數顯示區域開始 -->
      <div class="board">
        <h3 class="title">
          60 SECONDS CHALLENGE
        </h3>
        <div class="score">
          <span>
            SCORE
          </span>
          <span v-if="showScore">
            {{ getScore }}
          </span>
        </div>
      </div>
      <!-- 分數顯示區域結束 -->

      <!-- 倒數時間區域開始 -->
      <div 
        class="countdown"
        v-if="getTime"
      >
        {{ getTime }}
      </div>
      <!-- 倒數時間區域結束 -->

    </div>
    <!-- 遊戲資訊區域結束 -->

    <!-- 答題區域開始 -->
    <div class="answer-area">
      <div>
        <span class="num">
          {{ firstNum }}
        </span>
        <span class="operator">
          {{ operator }}
        </span>
        <span class="num">
          {{ lastNum }}
        </span>
        <span class="operator">=</span>
        <div class="anwser-box">
          <input 
            type="text"
            v-model="userAnswer"
            @keyup.enter="answerQuestion"
          >
        </div>
      </div>
    </div>
    <!-- 答題區域結束 -->

  </div>
</template>

<script>
// Enums
import FlowStatus from '../enum/flow-status.enum';
import OperatorType from '../enum/operator-type.enum';

import { setInterval, clearInterval } from 'timers';

export default {
  name: 'Main',
  data() {
    return {
      score: 0,
      firstNum: 0,
      lastNum: 0,
      operator: '',
      answer: '',
      userAnswer: '',
      gameTime: 60,
      timer: null
    }
  },
  methods: {
    /**
     * 發送終止遊戲的事件
     */
    endGame() {
      this.$emit('setScore', this.score);
      this.$emit('endGame', FlowStatus.END);
    },
    /**
     * 建立計算題目與答案
     */
    createArithmetic() {

      // 取得遊戲要計算的數字
      this.getRandowNumByTime();

      // 取得隨機運算符
      this.getRandomOperator();

      // 計算答案
      this.calcAnswer();
      
    },
    /**
     * 根據當下遊戲時間取得隨機數字
     */
    getRandowNumByTime() {

      if (this.gameTime >= 40) {

        // 前20秒為一位數計算
        this.firstNum = this.getRandom(1, 9);
        this.lastNum = this.getRandom(1, 9);

      } else if (
        this.gameTime < 40 &&
        this.gameTime >= 20
      ) {

        // 20~40秒為二位數計算
        this.firstNum = this.getRandom(10, 99);
        this.lastNum = this.getRandom(10, 99);

      } else {

        // 40~60秒為三位數計算
        this.firstNum = this.getRandom(100, 999);
        this.lastNum = this.getRandom(100, 999);

      }

    },
    /**
     * 於指定範圍取得隨機數字
     */
    getRandom(start, end) {
      return Math.floor(Math.random() * (end - start + 1)) + start;
    },
    /**
     * 取得隨機的運算符
     */
    getRandomOperator() {

      const operatorList = [
        OperatorType.PLUS,
        OperatorType.MINUS,
        OperatorType.MULTIPLY,
        OperatorType.DIVIDE,
      ];

      const randomNum = this.getRandom(0, 3);

      this.operator = operatorList[randomNum];

    },
    /**
     * 初始化時間
     */
    initTime() {

      this.timer = setInterval(() => {

        this.gameTime -= 1;

        if (this.gameTime === 0) {
          clearInterval(this.timer);
          this.endGame();
        }

      }, 1000);

    },
    /**
     * 計算題目的答案
     */
    calcAnswer() {

      switch (this.operator) {

        case OperatorType.PLUS:
          this.answer = this.firstNum + this.lastNum;
          break;

        case OperatorType.MINUS:
          this.answer = this.firstNum - this.lastNum;
          break;

        case OperatorType.MULTIPLY:
          this.answer = this.firstNum * this.lastNum;
          break;

        case OperatorType.DIVIDE:
          this.answer = this.firstNum / this.lastNum;
          break;

      }

    },
    /**
     * 玩家答題時，觸發的函式
     */
    answerQuestion() {

      if (this.userAnswer === String(this.answer)) {

        // 答題正確加分
        this.plusScore();
        
      } else {

        // 答題錯誤扣分
        this.minusScore();

      }

      this.userAnswer = '';
      this.createArithmetic();

    },
    /**
     * 加分數
     */
    plusScore() {
      
      if (this.gameTime >= 20) {
        this.score ++;
      } else {
        this.score += 5;
      }

    },
    /**
     * 扣分數
     */
    minusScore() {
      
      if (!this.score) {
        return;
      }

      this.score --;

    }
  },
  computed: {
    /**
     * 取得當前分數轉換的字串
     */
    getScore() {

      let fillZero = '';

      const currentScore = String(this.score);
      const fillLen = 3 - currentScore.length;

      for (let i = 0; i < fillLen; i ++) {
        fillZero += '0';
      }

      return `${fillZero}${currentScore}`;

    },
    /**
     * 是否顯示當前分數
     */
    showScore() {
      return this.score || this.score === 0;
    },
    /**
     * 取得字串化的時間
     */
    getTime() {

      let time = String(this.gameTime);

      if (time.length < 2) {
        time = '0' + time;
      }

      return `00:${time}`;

    }
  },
  mounted() {
    this.createArithmetic();
    this.initTime();
  },
  destroyed() {

    if (this.timer) {
      clearInterval(this.timer);
    }

  }
}
</script>

<style scoped lang="scss">
@import '../scss/mixin.scss';
.box {
  padding: 10px;
  width: 100%;
}
.board {
  margin-bottom: 40px;
  .title {
    margin: 0;
    border: 3px solid $white;
    padding: 10px;
    color: $white;
    font-weight: $primaryFontWeight;
    font-size: 20px;
  }
  .score {
    display: flex;
    align-items: center;
    span:first-child {
      padding: 10px;
      background-color: $white;
      color: $primaryOrange;
      font-weight: $primaryFontWeight;
      font-size: 20px;
    }
    span:last-child {
      margin-left: 10px;
      font-weight: $primaryFontWeight;
      font-size: 30px;
    }
  }
}
.countdown {
  margin-bottom: 40px;
  text-align: center;
  color: $white;
  font-size: 60px;
  font-weight: $primaryFontWeight;
  font-style: italic;
}
.answer-area {
  > div {
    display: flex;
    align-items: center;
    > * {
      line-height: 40px;
    }
  }
  .anwser-box {
    position: relative;

    > input {
      width: 180px;
      padding: 5px;
      font-size: 40px;
      font-weight: $primaryFontWeight;
    }

    &:after {
      content: 'press enter to answer';
      position: absolute;
      right: 0;
      left: 0;
      bottom: -20px;
      color: $white;
      line-height: 20px;
      text-align: center;
    }
    
  }
  font-weight: $primaryFontWeight;
  .num {
    font-size: 40px;
  }
  .operator {
    padding: 0 5px;
    font-size: 40px;
    color: $white;
  }
  p {
    margin: 0;
    text-align: right;
    color: $white;
    font-style: italic;
  }
}
@media all and (min-width: 768px) {
  .box {
    width: auto;
    > div:first-child {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 150px;
    }
  }
  .board {
    margin-bottom: 0;
    margin-right: 100px;
    .title {
      margin: 0;
    }
  }
  .countdown {
    margin-bottom: 0;
    font-size: 80px;
  }
  .answer-area {
    > div {
      > * {
        line-height: 70px;
      }
    }
    .anwser-box {

      > input {
        width: 300px;
        padding: 10px;
        font-size: 70px;
        line-height: 80px;
      }

    }
    .num {
      font-size: 70px;
    }
    .operator {
      padding: 0 10px;
      font-size: 70px;
    }
    p {
      font-size: 20px;
    }
  }
}
</style>
