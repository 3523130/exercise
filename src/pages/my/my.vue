<template>
  <view class="my">
     <view class="top">
      <view class="nav" :style="{height:navBarHeight + 'px'}"></view>
      <view class="head">
          <view class="welcome" v-if="!show">
              <view class="tit">终于等到你</view>
              <nut-button class="login-btn" @click="allow">登录</nut-button>
          </view>
          <view class="user" v-if="show">
              <view class="user-img"><img :src="userInfo.avatarUrl" alt=""></view>
              <view class="user-info">
                  <view class="user-info-name">{{ userInfo.nickName }}</view>
                  <view class="user-info-time">已在1天</view>
              </view>
              <nut-icon name="right"></nut-icon>
          </view>
      </view>
    </view>
    <view class="content">
        <view class="cell person">
            <view class="person-list" v-for="(icon, index) in userIcon" :key="index">
                <img  :src="icon.icon" alt="">
                <view>{{ icon.name }}</view>
            </view>
        </view>
    </view>
  </view>
</template>

<script>
import { reactive, toRefs, onMounted } from 'vue';
import Taro from '@tarojs/taro';
import badminton from '../../assets/images/badminton.svg'
import card from '../../assets/images/card.svg'
import money from '../../assets/images/money.svg'
import badminton2 from '../../assets/images/badminton2.svg'
export default {
  name: 'Index',
  components: {
    
  },
  setup(){
    const state = reactive({
      navBarHeight: 0,
      menuBotton: 0,
      menuRight: 0,
      menuHeight: 0,
      show: false,
      userIcon: [
        { icon: money, name: '钱包' },
        { icon: card, name: '卡包' },
        { icon: badminton2, name: '订单' },
      ],
      userInfo: {}
    });
    const allow = ()=> {
      // state.userName = '多肉葡萄'
      Taro.getUserProfile({
        desc: '用于完善会员资料', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
        success: (res) => {
          state.show = true
          state.userInfo = res.userInfo
          console.log(res.userInfo);
          // 开发者妥善保管用户快速填写的头像昵称，避免重复弹窗
        }
      })
    };
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
      card,
      money,
      badminton2,
      allow
    }
  }
}
</script>

<style lang="scss">
.my {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  // height: 100vh;
  .top{
    background: #2098f6;
    position: relative;
    height: 240px;
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
    .welcome{
        margin-top: 20px;
        padding: 0 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 18px;
        color: #fff;
        .login-btn{
            width: 80px;
            background-color: #fff;
            color: #2098f6;
            border: none;
            font-size: 14px;
        }
    }
    .user{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 10px;
        color: #fff;
        margin-top: 20px;
        .user-img{
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background-color: #fff;
            img{
                width: 60px;
                height: 60px;
                border-radius: 50%;
                margin-top: 5px;
            }
        }
        .user-info{
            text-align: left;
            width: 70%;
            height: 70px;
            line-height: 30px;
            text-indent: 10px;
        }
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
    .person{
      width: 95%;
      height: 100px;
    //   padding: 25px 15px;
      z-index: 10;
      position: absolute;
      overflow: hidden;
      top: 200px;
      left: 0;
      right: 0;
      display: flex;
      justify-content: space-around;
      align-items: center;
      .person-list{
          img{
              width: 40px;
              height: 40px;
          }
      }
    }
  }
}
.flex{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
