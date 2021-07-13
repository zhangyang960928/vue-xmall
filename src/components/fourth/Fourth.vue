<template>
  <div class="fourth">
    <div class="fourthWord">{{ list3.name }}</div>
    <div class="fourthWord1 displayF">
      <!-- 循环这个对象里面的图片 -->
      <!-- :class="{ fourthWord1one_wid: index === 0 }"  给下标为0的增加属性 -->
      <div
        class="fourthWord1one"
        v-for="(item, index) in list3.panelContents"
        :key="index"
        :class="{ fourthWord1one_wid: index === 0 }"
        @click="see(index, item.productId)"
      >
        <!-- 第一个图片大小不一致  v-if判断 是第一张  改变它的大小 -->
        <div v-if="index === 0" class="tool"></div>
        <img v-if="index === 0" :src="item.picUrl" alt="" class="oneimg" />
        <img :src="item.picUrl" alt="" class="twoimg" />
        <!-- 不是第一张  得加上价格 信息 -->
        <div v-if="index !== 0">
          <div class="fourthWord1two displayF justify-contentC align-itemsC">
            {{ item.productName }}
          </div>
          <div class="fourthWord1three displayF justify-contentC align-itemsC">
            {{ item.subTitle }}
          </div>
          <div class="fourthWord1four displayF justify-contentC align-itemsC">
            {{ item.salePrice.toFixed(2) }}
          </div>
          <div class="fourthWord1five displayF justify-contentC align-itemsC">
            <el-button
              style="width: 100px; height: 30px; padding: 8px"
              @click="index, item.productId"
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
  </div>
</template>

<script>
export default {
  name: "",
  props: {
    list3: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {};
  },
  components: {},
  methods: {
    // 传递id给详情页
    see(index,id) {
      if (index !== 0) {
        this.$router.push({
          path: "/Detail",
          query: {
            id: id,
          },
        });
        // console.log(id);
      }
    },
  },
  mounted() {
    // console.log(this.list3);
  },
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
.fourth {
  width: 1220px;
  height: 859px;
  border-radius: 8px;
  background: #fff;
  border-color: rgba(0, 0, 0, 0.14);
  margin-bottom: 30px;
  border: 1px solid #dcdcdc;
  .fourthWord {
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
  .fourthWord1 {
    width: 1220px;
    height: 800px;
    flex-wrap: wrap;
    overflow: hidden;
    .fourthWord1one {
      width: 25%;
      height: 400px;
      position: relative;
      background: white;
      .oneimg {
        width: 100%;
        height: 100%;
      }
      .twoimg {
        width: 206px;
        height: 206px;
        margin: 50px 49.5px 10px 49.5px;
      }
      .fourthWord1two {
        font-size: 16px;
        color: #424242;
        padding: 0 14px;
      }
      .fourthWord1three {
        font-size: 12px;
        color: #d0d0d0;
        padding: 10px;
      }
      .fourthWord1four {
        color: #d44d44;
        font-size: 18px;
        font-weight: 700;
        margin: 15px 0;
        height: 30px;
      }
      .fourthWord1five {
        margin: 15px 0;
        display: none;
      }
      &:hover {
        animation: fourthWord1one_move 0.3s linear forwards;
        .fourthWord1four {
          display: none;
        }
        .fourthWord1five {
          text-align: center;
          display: block;
        }
      }
    }
  }
}
.tool {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  &:hover {
    box-shadow: 0px 0px 20px 10px #eee inset;
  }
}
.fourthWord1one_wid {
  width: 50% !important;
  &:hover {
    animation: fourthWord1one_move1 0s linear forwards !important;
    box-shadow: inset 0px 0px 20px red !important;
  }
}
@keyframes fourthWord1one_move {
  0% {
    box-shadow: 0px 0px 0px #999;
    transform: translateY(0px);
  }
  100% {
    box-shadow: 0px 0px 20px #999;
    transform: translateY(-4px);
  }
}
@keyframes fourthWord1one_move1 {
  0% {
    transform: translateY(0px);
  }
  100% {
    transform: translateY(0px);
  }
}
</style>