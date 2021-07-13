<template>
  <div
    class="displayF flex-directionC justify-contentC align-itemsC"
    style="background: #ededed; padding-bottom: 50px"
  >
    <!-- 第一层 -->
    <div class="first first-right">
      <el-carousel trigger="click" height="500px" :autoplay="false">
        <!-- 循环list -->
        <el-carousel-item
          v-for="(item, index) in list"
          :key="index"
          class="aaa"
        >
          <!-- 父盒子设置相对定位 -->
          <h3 class="small">
            <!-- list里面每一个元素又是一个数组，再次循环它   此时的v-for应该是list的item -->
            <!-- 此时的图片是三张竖直排列的  设置绝对定位  让三张图片重合一起  实现效果 -->
            <!-- 循环图片的盒子设置绝对定位 -->
            <div
              style="width: 100%; height: 500px"
              v-for="(item1, index1) in item"
              :key="index1"
            >
              <!-- 图片引入的地址就是list的item的item1 -->
              <img
                style="
                  width: 100%;
                  height: 100%;
                  border-radius: 10px;
                  position: absolute;
                  top: 0px;
                "
                :src="item1"
                alt=""
              />
            </div>
          </h3>
        </el-carousel-item>
      </el-carousel>
    </div>
    <!-- 第二层 -->
    <div class="second displayF">
      <div class="secondWord" v-for="(item, index) in list1" :key="index">
        <div class="tool"></div>
        <img style="width: 304px; height: 200px" :src="item" alt="" />
      </div>
    </div>
    <!-- 第三层 -->
    <!-- v-if是保证传递给子组件有值 -->
    <thisrd v-if="list2" :name="list2"></thisrd>
    <!-- 第四层 -->
    <fourth v-if="list3" :list3="list3"></fourth>
    <!-- 第五层 -->
    <fourth v-if="list4" :list3="list4"></fourth>
    <!-- 第六层 -->
    <fourth v-if="list5" :list3="list5"></fourth>
    <!-- 第七层 -->
    <div class="second displayF">
      <div class="secondWord" v-for="(item, index) in list6" :key="index">
        <div class="tool"></div>
        <img style="width: 304px; height: 200px" :src="item" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import thisrd from "../components/third/Third";
import Fourth from "../components/fourth/Fourth.vue";
export default {
  name: "",
  props: {},
  data() {
    return {
      // 第一层参数
      list: [],
      // 第二层
      list1: [],
      // 第三层
      list2: null,
      // 第四层
      list3: null,
      // 第五层
      list4: null,
      // 第六层
      list5: null,
      // 第七层
      list6: [],
    };
  },
  components: {
    thisrd,
    Fourth,
  },
  methods: {
    getData() {
      axios
        .get("/api/goods/home")
        .then((res) => {
          console.log(res.data.data);
          // console.log(res.data.data[0].panelContents);
          // 循环轮播图的数组 有三个对象 每一个对象里面有三张图片
          res.data.data[0].panelContents.map((item) => {
            // 将格式转换成[1,2,3]
            let arr = [item.picUrl, item.picUrl2, item.picUrl3];
            // 过滤掉为空的图片
            arr = arr.filter((item1) => {
              return item1 !== "";
            });
            // console.log(arr);
            // 将循环拿到的三个arr增加到list里面
            // 格式变为[[1,2,3],[1,2,3],[1,2,3]]
            this.list.push(arr);
            // console.log(this.list);
          });
          // 活动版块
          this.list1 = res.data.data[1].panelContents.map((item) => {
            return item.picUrl;
          });
          // console.log(this.list1);
          // 热门商品
          this.list2 = res.data.data[2].panelContents;
          // 官方精选
          this.list3 = res.data.data[3];
          // 品牌周边
          this.list4 = res.data.data[4];
          // 品牌精选
          this.list5 = res.data.data[5];
          // 活动版块1
          this.list6 = res.data.data[6].panelContents.map((item) => {
            return item.picUrl;
          });
        })
        .catch((err) => {
          console.log("请求失败", err);
        });
    },
  },
  mounted() {
    this.getData();
  },
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
.first {
  .aaa:nth-child(2n) {
    .small {
      div:nth-child(2) {
        img {
          z-index: 999;
        }
      }
    }
  }
  width: 1220px;
  height: 500px;
  margin-top: 20px;
}
.second {
  width: 1220px;
  height: 200px;
  margin-top: 25px;
  border: 1px solid rgba(0, 0, 0, 0.14);
  border-radius: 8px;
  .secondWord {
    border-right: 1px solid rgba(0, 0, 0, 0.14);
    position: relative;
    &:nth-child(1) {
      img {
        border-top-left-radius: 8px !important;
        border-bottom-left-radius: 8px !important;
      }
    }
    &:nth-child(4) {
      img {
        border-top-right-radius: 8px !important;
        border-bottom-right-radius: 8px !important;
      }
    }
    &:hover {
      cursor: pointer;
    }
  }
  .secondWord:nth-child(4) {
    border-right: 0px !important;
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
</style>
