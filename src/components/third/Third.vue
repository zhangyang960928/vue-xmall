<template>
  <div class="third">
    <div class="thirdWord">热门商品</div>
    <div class="thirdWord1 displayF">
      <!-- 循环热门商品的数组 -->
      <div
        v-for="(item, index) in name"
        :key="index"
        class="thirdWord1one displayF flex-directionC align-itemsC"
      >
        <img :src="item.picUrl" alt="" />
        <div class="thirdWord1two">{{ item.productName }}</div>
        <div class="thirdWord1three">{{ item.subTitle }}</div>
        <div class="thirdWord1four">￥ {{ item.salePrice.toFixed(2) }}</div>
        <div class="thirdWord1five displayF">
          <el-button style="width: 100px; height: 30px; padding: 8px"
            >查看详情</el-button
          >
          <el-button
            type="primary"
            style="width: 100px; height: 30px; padding: 8px"
            >加入购物车</el-button
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  props: {
    name: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {};
  },
  components: {},
  methods: {},
  mounted() {},
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
.third {
  width: 1220px;
  height: 490px;
  margin-bottom: 30px;
  border-radius: 8px;
  background: #fff;
  border-color: rgba(0, 0, 0, 0.14);
  border: 1px solid #dcdcdc;
  margin-top: 30px;
  .thirdWord {
    padding-left: 30px;
    height: 60px;
    padding: 0 10px 0 24px;
    border-bottom: 1px solid #d4d4d4;
    font-size: 18px;
    color: #333;
    line-height: 60px;
    background: linear-gradient(#fbfbfb, #ececec);
    border-radius: 8px 8px 0 0;
  }
  .thirdWord1 {
    height: 430px;
    overflow: hidden;
    .thirdWord1one {
      width: 609px;
      height: 430px;
      img {
        width: 206px;
        height: 206px;
        margin: 50px 0 10px 0;
      }
      .thirdWord1two {
        font-size: 16px;
        color: #424242;
        padding: 0 14px;
      }
      .thirdWord1three {
        font-size: 12px;
        color: #d0d0d0;
        padding: 10px;
      }
      .thirdWord1four {
        color: #d44d44;
        font-size: 18px;
        font-weight: 700;
        margin: 15px 0;
        height: 30px;
      }
      .thirdWord1five {
        margin: 15px 0;
        display: none;
      }
      &:hover {
        animation: thirdWord1one_move 0.3s linear forwards;
        .thirdWord1four {
          display: none;
        }
        .thirdWord1five {
          display: block;
        }
      }
    }
  }
}
@keyframes thirdWord1one_move {
  0% {
    box-shadow: 0px 0px 0px #999;
    transform: translateY(0px);
  }
  100% {
    box-shadow: 0px 0px 20px #999;
    transform: translateY(-4px);
  }
}
</style>