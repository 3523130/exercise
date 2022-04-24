<template>
  <view class="home">
     <view class="top">
      <view class="nav" :style="{height:navBarHeight + 'px'}"></view>
      <view class="head"></view>
    </view>
    <div class="content">
      <view class="cell booking">
          <view class="place flex">
            <view class="region">深圳市</view>
            <view class="nearby" @click="skip">附近场所</view>
          </view>
          <div class="time flex">
            <view class="date">4月21日</view>
            <view class="time-frame">全天时段</view>
          </div>
          <view class="desc">区域/场馆/位置</view>
          <nut-button class="seek-btn">寻找场地</nut-button>
      </view>
      <view class="title">我的行程</view>
      <view class="cell route">
        <img :src="badminton" alt="">
        <view>您还没有行程，去订场吧~</view>
        <nut-button class="booking-btn">去订场</nut-button>
      </view>
    </div>
  </view>
</template>

<script>
import { reactive, toRefs, onMounted } from 'vue';
import Taro from '@tarojs/taro';
import badminton from '../../assets/images/badminton.svg'
export default {
  name: 'Home',
  components: {
    
  },
  setup(){
    const state = reactive({
      navBarHeight: 0,
      menuBotton: 0,
      menuRight: 0,
      menuHeight: 0,
    });
    const skip = ()=> {
      Taro.navigateTo({
        url: '/pages/searchSpace/searchSpace'
      })
    }
    onMounted(() => {
      let systemInfo = {}
      Taro.getSystemInfo({
        success: res => systemInfo = res
      })
      let menuButtonInfo = Taro.getMenuButtonBoundingClientRect()
      state.navBarHeight = (menuButtonInfo.top - systemInfo.statusBarHeight) * 2 + menuButtonInfo.height + systemInfo.statusBarHeight;
      state.menuBotton = menuButtonInfo.top - systemInfo.statusBarHeight;
      state.menuRight = systemInfo.screenWidth - menuButtonInfo.right;
      state.menuHeight = menuButtonInfo.height;
    })
    return {
      ...toRefs(state),
      badminton,
      skip
    }
  }
}
</script>

<style lang="scss">
.home {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  // height: 100vh;
  .top{
    background: #2098f6;
    position: relative;
    height: 303px;
  }
  .top::after{
    content: '';
    position: absolute;
    top: -192px;
    left: -131px;
    width: 292px;
    height: 283px;
    border-radius: 50%;
    background-color: #ececec;
    opacity: 0.25;
  }
  .head {
    // width: 100%;
    height: 218px;
    position: relative;
    overflow: hidden;
    &::after{
      content: '';
      position: absolute;
      bottom: -111px;
      right: -99px;
      width: 292px;
      height: 283px;
      border-radius: 50%;
      background-color: #ececec;
      opacity: 0.25;
    }
    &::before{
      content: '';
      position: absolute;
      bottom: -222px;
      right: 39px;
      width: 292px;
      height: 283px;
      border-radius: 50%;
      background-color: #ececec;
      opacity: 0.25;
    }
  }
  .content{
    // position: relative;
    .cell{
      background-color: #fff;
      box-shadow: 0px 2px 6px 0px #e0e0e0;
      border-radius: 15px;
      margin: 0 auto;
    }
    .booking{
      width: 85%;
      height: 160px;
      padding: 25px 15px;
      z-index: 10;
      position: absolute;
      overflow: hidden;
      top: 150px;
      left: 0;
      right: 0;
      .place{
        margin-bottom: 20px;
        .region{
          font-size: 18px;
          color: #000;
        }
        .nearby{
          font-size: 14px;
          color: #2196f3;
        }
      }
      .time{
        margin-bottom: 20px;
        .date{
          font-size: 20px;
          color: #000;
        }
        .time-frame{
          font-size: 16px;
          color: #000;
        }
      }
      .desc{
        color: #999;
        font-size: 14px;
        text-align: left;
      }
      .seek-btn{
        width: 100%;
        height: 40px;
        background-color: #2098f6;
        color: #fff;
        margin-top: 20px;
      }
    }
    .route{
      width: 93%;
      height: 120px;
      margin: 25px auto 0;
      padding: 20px 0;
      overflow: hidden;
      font-size: 14px;
      color: #2098f6;
      img{
        width: 50px;
        height: 50px;
      }
      .booking-btn{
        width: 180px;
        height: 40px;
        background-color: #2098f6;
        font-size: 14px;
        color: #fff;
        margin-top: 15px;
      }
    }
    .title{
      font-size: 16px;
      text-align: left;
      margin: 90px 0 0 10px;
    }
  }
  .nut-tabbar{
    // position: absolute;
    // bottom: 0;
  }
}
.flex{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
