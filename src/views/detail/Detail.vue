<template>
  <div>
    <div class="deta displayF flex-directionC align-itemsC">
      <div class="detail displayF">
        <!-- 侧边小图 -->
        <div class="detail1 displayF flex-directionC align-itemsC">
          <div
            class="detail2 displayF justify-contentC align-itemsC"
            v-for="(item, index) in list.productImageSmall"
            :key="index"
            @click="click(item, index)"
            :class="{ click_img: click_bor === index }"
          >
            <img :src="item" alt="" />
          </div>
        </div>
        <!-- 中间大图 -->
        <div class="detail3 displayF justify-contentE">
          <img :src="productImageBig" alt="" />
        </div>
        <!-- 右边部分 -->
        <div class="detail4">
          <div class="detail5">
            <div class="detail5Word1">{{ list.productName }}</div>
            <div class="detail5Word2 displayF justify-contentB">
              <div class="detail5Word3">{{ list.subTitle }}</div>
              <div class="detail5Word4">
                {{ Number(list.salePrice).toFixed(2) }}
              </div>
            </div>
          </div>
          <div class="detail6 displayF">
            <div class="detail6Word1">数量</div>
            <div
              class="detail6Word2"
              @click="remove"
              :class="{ disabled:num===1 }"
            >
              -
            </div>
            <input class="detail6Word3" type="text" v-model="num" @blur="blur"/>
            <div class="detail6Word2" @click="add">+</div>
          </div>
          <div class="detail7 displayF">
            <el-button type="primary" class="detail7Word">加入购物车</el-button>
            <el-button class="detail7Word">现在购买</el-button>
          </div>
        </div>
      </div>
      <!-- 底部 -->
      <div class="detail8">
        <div class="detail8Word1 displayF align-itemsC">产品信息</div>
        <div v-html="list.detail"></div>
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
      id: "",
      list: "",
      num: 1,
      productImageBig: "list.productImageBig",
      click_bor: "",
    };
  },
  components: {},
  methods: {
    getData() {
      axios
        .get(`/api/goods/detail?productId=${this.id}`)
        .then((res) => {
          // console.log(res);
          if (res.data.data.code === 200) {
            this.list = res.data.data.result;
            this.productImageBig = this.list.productImageBig;
            this.click_bor = 0;
            console.log(this.list);
          }
        })
        .catch((err) => {
          console.log("请求失败", err);
        });
    },
    click(item, index) {
      this.productImageBig = item;
      this.click_bor = index;
    },
    remove() {
      if (this.num <= 1) {
        this.num = 1;
      } else {
        this.num--;
      }
    },
    add() {
      this.num++;
    },
    blur(){
      if(this.num===''){
        this.num=1
      }
    }
  },
  mounted() {
    this.id = this.$route.query.id;
    // console.log(this.id);
    this.getData();
  },
  computed: {},
  watch: {
    num(val1,val2){
      if(Number(val1)>this.list.limitNum){
        this.num=val2
        this.$message.error(`购买数量不能超过${this.list.limitNum}`)
        return
      }
      if(!/^[1-9]\d*$/.test(val1)){
        this.num=''
        return
      }
      if(String(val1).includes('')){
        this.num=String(val1).trim()
        return
      }
    }
  },
};
</script>

<style lang='scss' scoped>
.deta {
  background: #ededed;
  .detail {
    width: 1220px;
    height: 563px;
    margin: 20px 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #dcdcdc;
    .detail1 {
      width: 86px;
      height: 440px;
      margin: 60px 0 0 60px;
      .click_img {
        border: 3px solid rgba(0, 0, 0, 0.2) !important;
      }
      .detail2 {
        width: 80px;
        height: 80px;
        border: 1px solid rgba(0, 0, 0, 0.2);
        border-radius: 5px;
        margin-bottom: 10px;
        &:hover {
          cursor: pointer;
        }
        img {
          width: 54px;
          height: 54px;
        }
      }
    }
    .detail3 {
      width: 460px;
      height: 440px;
      margin-top: 60px;
      img {
        width: 440px;
        height: 440px;
      }
    }
    .detail4 {
      width: 450px;
      height: 440px;
      margin-left: 10px;
      margin-top: 60px;
      .detail5 {
        width: 432px;
        height: 90px;
        padding: 8px 8px 18px 10px;
        .detail5Word1 {
          font-size: 24px;
          color: #000;
          margin-bottom: 13px;
        }
        .detail5Word3 {
          font-size: 14px;
          color: #bdbdbd;
        }
        .detail5Word4 {
          color: #d44d44;
          font-weight: 700;
          font-size: 16px;
        }
      }
      .detail6 {
        width: 450px;
        height: 80px;
        border-top: 1px solid #ebebeb;

        .detail6Word1 {
          margin-left: 10px;
          margin-top: 35px;
          font-size: 14px;
          color: #8d8d8d;
          margin-right: 20px;
        }
        .detail6Word2 {
          text-align: center;
          line-height: 22px;
          width: 25px;
          height: 25px;
          border: 1px solid #eee;
          border-radius: 50%;
          color: #666;
          font-size: 15px;
          font-weight: bold;
          margin-top: 32px;
          box-shadow: 0px 0px 10px #ececec;
          &:hover {
            cursor: pointer;
            background: #eee;
          }
        }
        .detail6Word3 {
          width: 36px;
          height: 18px;
          border: 0px;
          margin-top: 37px;
          text-align: center;
          padding: 0px 10px;
        }
      }
      .detail7 {
        width: 450px;
        height: 80px;
        border-top: 1px solid #ebebeb;
        .detail7Word {
          width: 145px;
          height: 50px;
          margin: 30px 10px 0 10px;
          font-size: 14px;
          &:nth-child(1) {
            background: #678ee7;
          }
        }
      }
    }
  }
  .detail8 {
    width: 1220px;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #dcdcdc;
    margin-bottom: 130px;
    .detail8Word1 {
      height: 60px;
      font-size: 18px;
      background: #f5f5f5;
      color: #626262;
      padding-left: 25px;
    }
  }
}
.disabled {
  &:hover {
    cursor: not-allowed !important;
  }
}
</style>