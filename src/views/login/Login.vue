<template>
  <div class="wrapper">
    <img
      class="wrapper__img"
      src="http://www.dell-lee.com/imgs/vue3/user.png" alt="用户注册头像"
    >
    <div class="wrapper__input">
      <input type="text" class="wrapper__input__content" placeholder="请输入手机号">
    </div>
    <div class="wrapper__input">
      <input type="password" class="wrapper__input__content" placeholder="请输入密码">
    </div>
    <div class="wrapper__login-button">登录</div>
    <div class="wrapper__login-link">立即注册</div>
  </div>
</template>

<script>
export default {
  name: 'Login'
}
</script>

<style lang="scss" scoped>
@import '../../style/variables.scss';

.wrapper {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  transform: translateY(-50%);
  &__img {
    display: block;
    width: .66rem;
    height: .66rem;
    margin: 0 auto .4rem auto;
  }
  &__input {
    width: 2.95rem;
    height: .48rem;
    margin: 0 auto .16rem auto;
    background: #F9F9F9;
    border: 1px solid rgba(0, 0, 0, 0.10);
    border-radius: 6px;
    &__content {
      box-sizing: border-box;
      width: 100%;
      padding: .12rem .16rem .12rem .16rem;
      border: none;
      outline: none;
      background: none;
      line-height: .24rem;
      color: $content-notice-fontColor;
      font-size: .16rem;
      &::placeholder {
        color: $content-notice-fontColor;
        font-size: .16rem;
      }
    }
  }
  &__login-button {
    //box-sizing: border-box;
    width: 2.95rem;
    //height: .48rem;
    //padding: .12rem 0;
    line-height: .48rem;
    margin: .32rem auto .16rem auto;
    border-radius: .04rem;
    background: #0091FF;
    box-shadow: 0 .04rem .08rem 0 rgba(0, 145, 255, 0.32);
    font-size: .16rem;
    color: #FFFFFF;
    text-align: center;
  }
  &__login-link {
    text-align: center;
    font-size: 14px;
    color: $content-notice-fontColor;
  }
}
</style>
