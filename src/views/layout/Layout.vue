<template>
  <div>
    <!-- 头部 -->
    <div class="top displayF justify-contentC">
      <div class="topWord displayF justify-contentB align-itemsC">
        <div class="topWord1 displayF justify-contentC align-itemsC">M</div>
        <div class="topWord2 topWord-height displayF align-itemsC">
          <el-autocomplete
            popper-class="my-autocomplete"
            v-model="state"
            placeholder="请输入内容"
            :fetch-suggestions="querySearch"
          >
            <i class="el-icon-search el-input__icon" slot="suffix"> </i>
          </el-autocomplete>
          <div class="topWord2one displayF justify-contentC align-itemsC">
            全部商品
          </div>
          <div class="topWord2two displayF justify-contentC align-itemsC">
            捐赠
          </div>
          <div class="topWord2three displayF align-itemsC">
            <i class="el-icon-user-solid"></i>
            <i class="el-icon-shopping-cart-full"></i>
            <div class="topWord2four displayF justify-contentC align-itemsC">
              0
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- 导航栏 -->
    <div class="hide displayF justify-contentC align-itemsC">
      <div class="hideWord displayF align-itemsC">
        <div
          v-for="(item, index) in list"
          :key="index"
          class="box displayF align-itemsC"
        >
          <div class="hideWord1"></div>
          <div class="hideWord3">{{ item.name }}</div>
        </div>
      </div>
    </div>
    <router-view></router-view>
    <!-- 底部 -->
    <div class="foot displayF flex-directionC justify-contentC align-itemsC">
      <div class="footWord displayF">
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">订单服务</div>
          <div class="footWord1two">购买指南</div>
          <div class="footWord1two">支付方式</div>
          <div class="footWord1two">送货政策</div>
        </div>
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">服务支持</div>
          <div class="footWord1two">官方开源</div>
          <div class="footWord1two">项目前端</div>
          <div class="footWord1two">项目后端</div>
        </div>
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">自助服务</div>
          <div class="footWord1two">个人博客</div>
          <div class="footWord1two">个人简介</div>
          <div class="footWord1two">个人视频</div>
        </div>
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">其他项目</div>
          <div class="footWord1two">XPay支付系统</div>
          <div class="footWord1two">数据共享</div>
          <div class="footWord1two">待开发...</div>
        </div>
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">友情链接</div>
          <div class="footWord1two">宇cccc</div>
          <div class="footWord1two">Smartisan</div>
          <div class="footWord1two">Vue</div>
        </div>
        <div class="footWord1 displayF flex-directionC">
          <div class="footWord1one">关注我吧</div>
          <div class="footWord1two">腾讯 QQ</div>
          <div class="footWord1two">新浪微博</div>
          <div class="footWord1two">官方邮箱</div>
        </div>
        <div class="footWord2 displayF flex-directionC align-itemsE">
          <div class="footWord2One">1012139570</div>
          <div class="footWord2Two">
            周一至周日 10:00-23:00（限Starrer或捐赠人联系）
          </div>
          <div class="footWord2Three displayF justify-contentC align-itemsC">
            在线帮助
          </div>
        </div>
      </div>
      <div class="footWord1 displayF align-itemsE">
        <div class="footWord1One">
          Copyright ©2017, exrick.cn Co., Ltd. All Rights
          Reserved.本网站设计内容大部分属锤子科技
        </div>
        <div class="footWord1Two">法律声明</div>
        <div class="footWord1Three">隐私条款</div>
        <div class="footWord1Three">开发者中心</div>
      </div>
      <div class="footWord2 displayF align-itemsE">
        <div class="footWordOne">蜀ICP备16030308号-1</div>
        <div class="footWordOne">蜀ICP证16030308号</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  props: {},
  data() {
    return {
      state: "",
      list: [
        {
          name: "首页",
        },
        {
          name: "全部",
        },
        {
          name: "捐赠名单",
        },
        {
          name: "后台管理系统",
        },
        {
          name: "XMall小程序",
        },
        {
          name: "XPay支付系统",
        },
        {
          name: "XBoot开发平台",
        },
        {
          name: "宣传视频",
        },
        {
          name: "Github",
        },
        {
          name: "商用授权",
        },
      ],
    };
  },
  components: {},
  methods: {
    querySearch() {},
  },
  mounted() {},
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
.top {
  height: 100px;
  background: black;
  .topWord {
    width: 1220px;
    height: 100px;
    .topWord1 {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: white;
      color: black;
      margin-left: 5px;
      font-size: 25px;
    }
    .topWord2 {
      width: 700px;
      height: 36px;
      .topWord2one {
        width: 100px;
        font-size: 14px;
        color: #c8c8c8;
        margin-left: 10px;
      }
      .topWord2two {
        width: 100px;
        font-size: 14px;
        color: #c8c8c8;
        margin-left: 10px;
        border-right: 1px solid #c8c8c8;
      }
      .el-icon-user-solid {
        color: #999999;
        font-size: 20px;
        margin-left: 50px;
      }
      .el-icon-shopping-cart-full {
        color: #999999;
        font-size: 20px;
        margin-left: 50px;
      }
      .topWord2four {
        background: #9a9a9a;
        color: white;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        margin-left: 5px;
      }
    }
  }
}
.hide {
  height: 90px;
  background: #f7f7f7;
  .hideWord {
    width: 1220px;
    height: 90px;
    .box:nth-child(1){
      .hideWord3 {       
        padding: 0 10px;
      }
    }
    .hideWord1 {
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background: #bdbdbd;
      margin-right: 10px;
    }
    .hideWord2 {
      color: #666666;
      font-size: 14px;
      padding: 0 10px;
      margin-right: 10px;
      &:hover {
        cursor: pointer;
        font-weight: bold;
      }
    }
    .hideWord3 {
      color: #666666;
      font-size: 14px;
      margin-right: 10px;
      &:hover {
        cursor: pointer;
        font-weight: bold;
      }
    }
  }
}
.foot {
  padding: 50px 0 20px;
  border-top: 1px solid #e6e6e6;
  background: #fafafa;
  height: 350px;
  .footWord {
    width: 1220px;
    height: 180px;
    padding-top: 50px;
    border-bottom: 1px solid #e6e6e6;
    .footWord1 {
      width: 150px;
      height: 120px;
      .footWord1one {
        color: #646464;
        font-size: 12px;
        padding: 0 0 14px;
      }
      .footWord1two {
        color: #c3c3c3;
        font-size: 12px;
        padding: 6px 0;
        &:hover {
          cursor: pointer;
        }
      }
    }
    .footWord2 {
      width: 320px;
      height: 120px;
      .footWord2One {
        color: #646464;
        font-size: 30px;
      }
      .footWord2Two {
        font-size: 12px;
        color: #c3c3c3;
        width: 241px;
        margin-top: 5px;
      }
      .footWord2Three {
        width: 130px;
        height: 34px;
        font-size: 14px;
        color: #5079d9;
        border: 1px solid #dcdcdc;
        margin-top: 8px;
        border-radius: 4px;
        &:hover {
          background: #f1f1f1;
          cursor: pointer;
        }
      }
    }
  }
  .footWord1 {
    width: 1220px;
    height: 55px;
    .footWord1One {
      font-size: 12px;
      color: #757575;
    }
    .footWord1Two {
      font-size: 12px;
      color: #5049d9;
      padding: 1px 10px 0;
      border-left: 1px solid #ccc;
      margin-left: 10px;
      &:hover {
        cursor: pointer;
      }
    }
    .footWord1Three {
      font-size: 12px;
      color: #5049d9;
      padding: 1px 10px 0;
      border-left: 1px solid #ccc;
      &:hover {
        cursor: pointer;
      }
    }
  }
  .footWord2 {
    width: 1220px;
    height: 30px;
    .footWordOne {
      margin-right: 20px;
      color: #bdbdbd;
      font-size: 12px;
      &:hover {
        cursor: pointer;
      }
    }
  }
}
</style>