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
          <span>
            001
          </span>
        </div>
      </div>
      <!-- 分數顯示區域結束 -->

      <!-- 倒數時間區域開始 -->
      <div class="countdown">
        00:59
      </div>
      <!-- 倒數時間區域結束 -->

    </div>
    <!-- 遊戲資訊區域結束 -->

    <!-- 答題區域開始 -->
    <div class="answer-area">
      <div>
        <span class="num">333</span>
        <span class="operator">x</span>
        <span class="num">333</span>
        <span class="operator">=</span>
        <input type="text">
      </div>
      <p>
        press enter to answer
      </p>
    </div>
    <!-- 答題區域結束 -->

  </div>
</template>

<script>
export default {
  name: 'Main'
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
    > input {
      width: 180px;
      padding: 5px;
      font-size: 40px;
      font-weight: $primaryFontWeight;
    }
    > * {
      line-height: 40px;
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
      > input {
        width: 300px;
        padding: 10px;
        font-size: 70px;
        line-height: 80px;
      }
      > * {
        line-height: 70px;
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
