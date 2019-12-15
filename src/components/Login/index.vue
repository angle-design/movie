<template>
  <div class="login_body">
    <div>
      <input type="text" class="login_text" placeholder="账户名/手机号/email">
    </div>
    <div>
      <input type="password" class="login_text" placeholder="请输入您的密码">
    </div>
    <div class="login_btn">
      <input type="summit" value="登录">
    </div>
    <div class="login_link">
      <a href="#">立即注册</a>
      <a href="#">找回密码</a>
    </div>
  </div>
</template>

<script>
    export default {
        name: "login"
    }
</script>

<style scoped lang="less">
  .login_body {
    width: 100%;

    div {
      .login_text {
        width: 96%;
        height: 0.8rem;
        border: none;
        border-bottom: 0.02rem #ccc solid;
        margin:0 0 0.1rem 2%;
        font-size:0.32rem;
      }

      &.login_btn {
        height: 1rem;
        margin: 0.2rem;

        input {
          width: 100%;
          height: 100%;
          background: #e54847;
          border-radius: 0.06rem;
          border: none;
          display: flex;
          color:#fff;
          text-align: center;
          font-size:0.32rem;
        }
      }

      &.login_link {
        display: flex;
        justify-content: space-between;

        a {
          text-decoration: none;
          margin: 0 0.1rem;
          font-size: 0.24rem;
          color: #e54847;
        }
      }
    }
  }
</style>
