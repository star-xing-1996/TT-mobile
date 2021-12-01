<template>
  <div class="login-container">
    <!-- 导航栏 -->
    <van-nav-bar class="page-nav-bar" title="登录" />
    <!-- 表单项 -->
    <van-form @submit="onSubmit">
      <van-field
        v-model="user.username"
        label="用户名"
        placeholder="用户名"
        :rules="[{ required: true, message: '请填写用户名' }]"
      >
        <i slot="left-icon" class="iconfont icon-shouji"></i>
      </van-field>
      <van-field
        v-model="user.code"
        name="密码"
        label="验证码"
        placeholder="密码"
        :rules="[{ required: true, message: '请填写密码' }]"
      >
        <i slot="left-icon" class="iconfont icon-yanzhengma"></i>
        <template #button>
          <van-button class="send-sms-btn" round size="small" type="primary"
            >发送验证码</van-button
          >
        </template>
      </van-field>
      <div style="margin: 16px" class="login-btn-wrap">
        <van-button
          round
          block
          type="info"
          native-type="submit"
          class="login-btn"
          >提交</van-button
        >
      </div>
    </van-form>
  </div>
</template>

<script>
import { login } from "@/api/user.js";
export default {
  name: "LoginPage",
  components: {},
  props: {},
  data() {
    return {
      user: {
        username: "13911111111",
        code: "246810",
      },
    };
  },
  methods: {
    async onSubmit() {
      try {
        const res = await login(this.user);
        console.log("登录成功", res);
      } catch (err) {
        if (err.response.status === 400) {
          console.log("登录失败", err);
        }
      }
    },
  },
};
</script>

<style lang="less" scoped>
.login-container {
  font-size: 16px;
  .iconfont {
    font-size: 37px;
  }
}
.send-sms-btn {
  // width: 152px;
  // height: 46px;
  // line-height: 46px;
  background-color: #ededed;
  font-size: 22px;
  color: #666;
  border: #ededed;
}
.login-btn-wrap {
  padding: 53px 33px;
  .login-btn {
    background-color: #6db4fb;
    border: none;
  }
}
</style>
