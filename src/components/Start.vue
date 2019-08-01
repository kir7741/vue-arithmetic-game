<template>
  <div>

    <!-- logo 區域開始 -->
    <h1 class="logo">
      <div>60</div>
      <div>
        <span>SECONDS</span>
        <span>CHALLENGE</span>
        <span class="sign">+−×÷</span>
      </div>
    </h1>
    <!-- logo 區域結束 -->

    <!-- 按鈕區域開始 -->
    <div class="btn-group">
      <button type="button">
        START!
      </button>
      <p>try to answer more as you can</p>
    </div>
    <!-- 按鈕區域結束 -->

  </div>
</template>

<script>
export default {
  name: 'Start'
}
</script>

<style scoped lang="scss">
@import '../scss/mixin.scss';
.logo {
  display: flex;
  justify-content: center;
  margin: 0;
  font-weight: $primaryFontWeight;
  div:nth-child(1) {
    margin-right: 10px;
    color: $white;
    font-size: 95px;
    text-shadow: 5px 0px $black;
  }
  div:nth-child(2) {
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    font-size: 35px;
  }
  .sign {
    position: absolute;
    top: 22px;
    right: 0;
    border-bottom: 6px double $white;
    color: $white;
    font-size: 14px;
  }
}
.btn-group {
  margin-top: 30px;
  button {
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
  p {
    margin: 10px 0 0 0;
    color: $white;
    font-size: 18px;
    font-weight: bold;
  }
}
@media all and (min-width: 768px) {
  .logo {
    div:nth-child(1) {
      margin-right: 15px;
      font-size: 150px;
      text-shadow: 8px 0px $black;
    }
    div:nth-child(2) {
      font-size: 55px;
    }
    .sign {
      top: 40px;
      font-size: 23px;
    }
  }
  .btn-group {
    button {
      width: 350px;
      font-size: 30px;
    }
    p {
      font-size: 18px;
    }
  }

} 
@media all and (min-width: 1024px) {
  .logo {
    div:nth-child(1) {
      margin-right: 15px;
      font-size: 200px;
      text-shadow: 10px 0px $black;
    }
    div:nth-child(2) {
      font-size: 60px;
    }
    .sign {
      top: 70px;
      font-size: 25px;
    }
  }
  .btn-group {
    button {
      font-size: 36px;
    }
    p {
      font-size: 20px;
    }
  }
} 
</style>