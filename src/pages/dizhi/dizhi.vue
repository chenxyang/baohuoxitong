<template>
    <div class="dizhi">
        <div class="address">
            <div class="item" v-for="item in list" @click="setDefault(item.code)">
                <img src="../../assets/imgs/shouhuodizhi@2x.png"  class="left">
                <p class="name-mobile">
                    <span>姓名：{{item.receiver}}</span>
                    <i>电话：{{item.mobile}}</i>
                </p>
                <p class="address">
                    收货地址：<i>{{item.province}}</i> <i>{{item.city}}</i> <i>{{item.area}}</i> {{item.address}}
                </p>
            </div>
        </div>
        <div class="footer" @click="$router.push('/tianjiadizhi')">添加地址</div>
    </div>
</template>
<script>
import { queryAddress, setDefultAddress } from "api/baohuo";
export default {
  data() {
    return {
      list: []
    };
  },
  methods: {
    setDefault(code) {
      setDefultAddress(code).then(res => {
        if (res) {
          if (this.$route.query.address === "1") {
            this.$router.push("/xuangoushangpin/shangpingoumai?code=" + code);
          } else if (this.$route.query.address === "2") {
            this.$router.push("/buyCloud/tijiaodingdan?code=" + code);
          } else if (this.$route.query.address === "3") {
            this.$router.push("/woyaochuhuo?code=" + code);
          }
        }
      });
    }
  },
  mounted() {
    queryAddress().then(res => {
      this.list = res;
    });
  }
};
</script>
<style lang="scss" scoped>
@import "../../common/scss/variable.scss";
.dizhi {
  .address {
    margin-bottom: 1rem;
  }
  .item {
    height: 1.8rem;
    padding: 0.3rem 0.8rem;
    background-color: #fff;
    position: relative;
    border-bottom: 1px solid #eee;
    img {
      width: 0.3rem;
      position: absolute;
      top: 50%;
      right: 0.3rem;
      transform: translateY(-50%);
      &.left {
        left: 0.28rem;
      }
      &.right {
        width: 0.2rem;
      }
    }
    .name-mobile {
      position: relative;
      i {
        position: absolute;
        left: 2.7rem;
      }
    }
    p {
      font-size: $font-size-medium;
      color: #333;
      &.address {
        margin-top: 0.24rem;
        font-size: $font-size-small;
        line-height: 0.4rem;
      }
    }
  }
  .footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    line-height: 1rem;
    text-align: center;
    background-color: $primary-color;
    color: #fff;
    font-size: $font-size-large-ss;
  }
}
</style>
