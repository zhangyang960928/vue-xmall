<template>
  <div class="register displayF justify-contentC align-itemsC">
    <div class="registerBox">
      <div class="registerWord1 displayF justify-contentC align-itemsC">
        注册 XMall 账户
      </div>
      <div class="registerWord2">
        <el-input
          v-model="input"
          placeholder="账户"
          class="input common"
        ></el-input>
        <el-input
          placeholder="密码"
          v-model="input1"
          type="password"
          class="input common"
        ></el-input>
        <el-input
          placeholder="重复密码"
          v-model="input2"
          type="password"
          class="input common"
        ></el-input>
        <div class="argee">
          <el-checkbox v-model="checked" size="medium" class="checkbox-border"
            >我已阅读并同意遵守
            <el-link type="primary" :underline="false" class="law"
              >法律声明</el-link
            >
            和
            <el-link type="primary" :underline="false" class="privacy"
              >隐私条款</el-link
            >
          </el-checkbox>
        </div>
        <div>
          <el-button
            :type="info"
            class="onebut"
            :disabled="disabled"
            @click="register"
            >注册</el-button
          >
        </div>
        <div class="foot displayF justify-contentC align-itemsC">
          如果您已拥有 XMall 账户，则可在此
          <el-link
            type="primary"
            :underline="false"
            class="foot1"
            @click="login"
            >登录</el-link
          >
        </div>
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
      input: "",
      input1: "",
      input2: "",
      checked: "false",
      info: "info",
      disabled: true,
      checked: false,
    };
  },
  components: {},
  methods: {
    // 点击底部登录
    login() {
      this.$notify.info({
        title: "登录提示",
        message: "测试体验账号密码：test | test",
      });
      this.$router.push("/login");
    },
    // 点击法律声明
    law() {
      this.$notify.info({
        title: "法律声明",
        message:
          "此仅为个人练习开源模仿项目，仅供学习参考，承担不起任何法律问题",
      });
    },
    // 点击隐私条款
    privacy() {
      this.$notify.info({
        title: "隐私条款",
        message:
          "本网站将不会严格遵守有关法律法规和本隐私政策所载明的内容收集、使用您的信息",
      });
    },
    // 点击注册
    register() {
      if (this.checked === false) {
        this.$message.error("您未勾选同意我们的相关注册协议!");
        return;
      }
      if (this.input1 !== this.input2) {
        this.$message.error("两次输入的密码不相同!");
        return;
      }
      axios
        .post("/api/users/register", {
          username: this.input,
          password: this.input1,
        })
        .then((res) => {
          // console.log(res);
          if (res.data.code === 200) {
            this.$message.success("注册成功");
            this.$router.push("/login");
          }else{
            this.$message.error(res.data.message)
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
    // 监听账户
    input(val1, val2) {
      if (/.*[\u4e00-\u9fa5]+.*$/.test(val1)) {
        this.input = val2;
      } else {
        if (val1 && this.input1 && this.input2) {
          this.disabled = false;
          this.info = "primary";
        } else {
          this.disabled = true;
          this.info = "info";
        }
      }
    },
    // 监听密码
    input1(val1, val2) {
      if (val1 && this.input && this.input2) {
        this.disabled = false;
        this.info = "primary";
      } else {
        this.disabled = true;
        this.info = "info";
      }
    },
    // 监听重复密码
    input2(val1, val2) {
      if (val1 && this.input && this.input1) {
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
.register {
  height: 100%;
  background: #f7f7f7;
  .registerBox {
    width: 450px;
    height: 500px;
    border: 1px #eee solid;
    border-radius: 10px;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
    background: white;
    .registerWord1 {
      color: #666;
      font-size: 20px;
      height: 60px;
      font-weight: 700;
      border-bottom: 1px solid #dcdcdc;
    }
    .registerWord2 {
      margin-top: 50px;
      .common {
        width: 370px;
        margin-bottom: 15px;
        margin-left: 40px;
      }
      .argee {
        color: #999;
        margin-left: 40px;
      }
      .onebut {
        width: 370px;
        height: 50px;
        font-size: 20px;
        color: white;
        margin-left: 40px;
        margin-top: 20px;
      }
      .foot {
        width: 370px;
        height: 50px;
        margin-left: 40px;
        border-top: 1px solid #ccc;
        margin-top: 30px;
        font-size: 12px;
        color: rgb(153, 153, 153);
        .foot1 {
          font-size: 12px;
          margin-left: 10px;
        }
      }
    }
  }
}
</style>