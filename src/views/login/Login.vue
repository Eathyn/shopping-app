<template>
  <div class="wrapper">
    <img class="wrapper__img"
         src="http://www.dell-lee.com/imgs/vue3/user.png" alt="用户注册头像">
    <div class="wrapper__input">
      <input type="text" class="wrapper__input__content" placeholder="请输入用户名" v-model="username"
             autocomplete="new-password">
    </div>
    <div class="wrapper__input">
      <input type="password" class="wrapper__input__content" placeholder="请输入密码" v-model="password"
             autocomplete="new-password">
    </div>
    <div class="wrapper__login-button" @click="handleLogin">登录</div>
    <div class="wrapper__login-link" @click="handleRegisterClick">立即注册</div>
    <Toast v-if="show" :message="toastMessage" />
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import { useRouter } from 'vue-router'
import { post } from '../../utils/request'
import Toast, { useToastEffect } from '../../components/Toast'

// user login
const useLoginEffect = (showToast) => {
  const router = useRouter()
  const data = reactive({ username: '', password: '' })

  const handleLogin = async () => {
    const { username, password } = data
    // verify
    if (username === '') {
      showToast('用户名为空')
      return
    } else if (password === '') {
      showToast('密码为空')
      return
    }
    // send request
    try {
      const result = await post('/api/user/login', { username, password })
      if (result?.errno === 0) {
        localStorage.isLogin = true
        await router.push({ name: 'Home' })
      } else {
        showToast('登录失败')
      }
    } catch (err) {
      showToast('请求失败')
    }
  }
  const { username, password } = toRefs(data)
  return { username, password, handleLogin }
}

// redirect to register page
const useRegisterEffect = () => {
  const router = useRouter()
  const handleRegisterClick = () => {
    router.push({ name: 'Register' })
  }
  return { handleRegisterClick }
}

export default {
  name: 'Login',
  components: {
    Toast
  },
  setup () {
    const { show, toastMessage, showToast } = useToastEffect()
    const { username, password, handleLogin } = useLoginEffect(showToast)
    const { handleRegisterClick } = useRegisterEffect()
    return {
      username,
      password,
      show,
      toastMessage,
      handleLogin,
      handleRegisterClick
    }
  }
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
