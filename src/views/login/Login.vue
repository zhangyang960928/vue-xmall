<template>
  <div class="login displayF justify-contentC align-itemsC">
    <div class="box">
      <div class="login1 displayF justify-contentC align-itemsC">
        <div class="loginImg displayF justify-contentC align-itemsC">M</div>
      </div>
      <div class="login2 displayF justify-contentC align-itemsC">
        使用 XMall 账户 登录官网
      </div>
      <!-- 账户、密码框 -->
      <div class="login2">
        <el-form class="ruleinput">
          <el-form-item prop="username">
            <el-input
              v-model="username"
              placeholder="账户"
              class="input"
            ></el-input>
          </el-form-item>
          <el-form-item prop="password">
            <el-input
              type="password"
              v-model="password"
              placeholder="密码"
              class="input"
            ></el-input>
          </el-form-item>
        </el-form>
      </div>
      <!-- 注册、忘记密码框 -->
      <div class="login3 displayF align-itemsC">
        <el-checkbox class="checkcolor" size="smmedium" v-model="checked"
          >记住密码</el-checkbox
        >
        <el-link :underline="false" type="primary" class="bor" @click="register"
          >注册 XMall 账户</el-link
        >
        <el-link :underline="false" type="primary" @click="remove"
          >忘记密码
        </el-link>
      </div>
      <!-- 底部 -->
      <div>
        <el-button
          :type="info"
          class="onebut"
          :disabled="disabled"
          @click="login"
          >登录</el-button
        >
      </div>
      <div>
        <el-button type="info" class="onebut1" @click="back">返回</el-button>
      </div>
      <div class="foot displayF">
        <div class="word">其他账户登录:</div>
        <i class="iconfont icon-weixin" @click="weixin"></i>
        <i class="iconfont icon-weibo1193419easyiconnet" @click="weibo"></i>
        <i class="iconfont icon-QQ" @click="QQ"></i>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "",
  props: {},
  data() {
    return {
      checked: false,
      username: "",
      password: "",
      disabled: true,
      info: "info",
    };
  },
  components: {},
  methods: {
    // 点击找回密码  侧边弹框
    remove() {
      this.$notify.info({
        title: "找回密码",
        message: "请联系作者邮箱找回密码或使用测试账号登录：test | test",
      });
    },
    // 点击微信
    weixin() {
      this.$notify.info({
        title: "待开发",
        message: "此功能开发中...",
      });
    },
    // 点击微博
    weibo() {
      this.$notify.info({
        title: "待开发",
        message: "此功能开发中...",
      });
    },
    // 点击QQ
    QQ() {
      this.$notify.info({
        title: "待开发",
        message: "此功能开发中...",
      });
    },
    // 点击返回
    back() {
      this.$router.back();
    },
    // 点击注册
    register() {
      this.$router.push("/register");
    },
    // 点击登录
    login() {
      axios
        .post("/api/users/login", {
          username: this.username,
          password: this.password,
        })
        .then((res) => {
          console.log(res);
          if (res.data.code === 200) {
            console.log(res.data.data);
            this.$message.success("登录成功");
            // 储存账户密码  转成字符串
            localStorage.setItem("vue-name", JSON.stringify(res.data.data.user));
            // 跳转主页面
            this.$router.push("/");
          }
        })
        .catch((err) => {
          console.log("请求失败", err);
        });
    },
  },
  mounted() {},
  computed: {},
  watch: {
    // 监听账户、密码的变化 如果有一个为空 则登录一直显示禁用状态  不为空 则变成蓝色状态的可点框
    username(val1, val2) {
      if (val1 && this.password) {
        this.disabled = false;
        this.info = "primary";
      } else {
        this.disabled = true;
        this.info = "info";
      }
    },
    password(val1, val2) {
      if (val1 && this.username) {
        this.disabled = false;
        this.info = "primary";
      } else {
        this.disabled = true;
        this.info = "info";
      }
    },
  },
};
</script>

<style lang='scss' scoped>
.login {
  height: 100%;
  background: #f7f7f7;
}
.box {
  width: 450px;
  height: 650px;
  border: 1px #eee solid;
  border-radius: 10px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  background: white;
  .login1 {
    width: 450px;
    height: 140px;
    margin-top: 20px;
    .loginImg {
      width: 80px;
      height: 80px;
      background: red;
      border-radius: 50%;
      font-size: 50px;
      color: white;
    }
  }
  .login2 {
    font-size: 20px;
    color: #666;
  }
  .ruleinput {
    margin: 50px 40px 0px 40px;
  }
}
.checkcolor {
  color: #999;
  margin-left: 40px;
}
.bor {
  border-right: 1px solid #ccc;
  padding-right: 10px;
  margin-right: 15px;
  margin-left: 90px;
}
.onebut {
  width: 370px;
  height: 50px;
  font-size: 20px;
  color: white;
  margin-left: 40px;
  margin-top: 20px;
}
.onebut1 {
  width: 370px;
  height: 50px;
  font-size: 20px;
  color: #646464;
  margin-left: 40px;
  margin-top: 20px;
  background: white;
  border: 1px solid #e1e1e1;
  &:hover {
    background: #eee;
  }
}
.foot {
  width: 370px;
  height: 50px;
  border-top: 1px solid #ccc;
  margin-left: 40px;
  margin-top: 40px;
}
.word {
  padding: 20px 5px 0 0;
  font-size: 12px;
  color: #999;
}
.icon-weixin {
  margin: 20px 10px 0 0;
  color: #999;
  &:hover {
    cursor: pointer;
  }
}
.icon-weibo1193419easyiconnet {
  margin: 20px 10px 0 0;
  color: #999;
  &:hover {
    cursor: pointer;
  }
}
.icon-QQ {
  margin: 20px 10px 0 0;
  color: #999;
  &:hover {
    cursor: pointer;
  }
}
</style>