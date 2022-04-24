<template>
  <view class="searchSpace">
     <nut-searchbar v-model="searchValue">
        <template v-slot:leftin>
        <nut-icon size="14" name="search2"></nut-icon>
        </template>
    </nut-searchbar>
    <view class="content">
        <view class="list">
            <view class="list-info">
                <img :src="spcae" alt="" class="list-info-img">
                <view class="list-info-name">sunny羽毛球馆</view>
                <view class="distance"><img :src="distance" alt=""><p>11km</p></view>
            </view>
            <view class="list-place"><img :src="place" alt=""><p>深圳市宝安区新安街道</p></view>
            <view class="list-price">
                <p>￥50起</p>
                <nut-button type="info" class="booking-btn">信息按钮</nut-button>
            </view>
        </view>
        <view class="list">
            <view class="list-info">
                <img :src="spcae" alt="" class="list-info-img">
                <view class="list-info-name">sunny羽毛球馆</view>
                <view class="distance"><img :src="distance" alt=""><p>11km</p></view>
            </view>
            <view class="list-place"><img :src="place" alt=""><p>深圳市宝安区新安街道</p></view>
            <view class="list-price">
                <p>￥50起</p>
                <nut-button type="info" class="booking-btn">信息按钮</nut-button>
            </view>
        </view>
        <view class="list">
            <view class="list-info">
                <img :src="spcae" alt="" class="list-info-img">
                <view class="list-info-name">sunny羽毛球馆</view>
                <view class="distance"><img :src="distance" alt=""><p>11km</p></view>
            </view>
            <view class="list-place"><img :src="place" alt=""><p>深圳市宝安区新安街道</p></view>
            <view class="list-price">
                <p>￥50起</p>
                <nut-button type="info" class="booking-btn">信息按钮</nut-button>
            </view>
        </view>
        <view class="list">
            <view class="list-info">
                <img :src="spcae" alt="" class="list-info-img">
                <view class="list-info-name">sunny羽毛球馆</view>
                <view class="distance"><img :src="distance" alt=""><p>11km</p></view>
            </view>
            <view class="list-place"><img :src="place" alt=""><p>深圳市宝安区新安街道</p></view>
            <view class="list-price">
                <p>￥50起</p>
                <nut-button type="info" class="booking-btn">信息按钮</nut-button>
            </view>
        </view>
    </view>
  </view>
</template>

<script>
import { reactive, toRefs, onMounted } from 'vue';
import spcae from '../../assets/images/space.jpg'
import distance from '../../assets/images/distance.svg'
import place from '../../assets/images/place.svg'
export default {
  name: 'searchSpace',
  components: {
    
  },
  setup(){
    const state = reactive({
        searchValue: ""
    });
    onMounted(() => {
      
    })
    return {
      ...toRefs(state),
      spcae,
      distance,
      place
    }
  }
}
</script>

<style lang="scss">
.searchSpace {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  text-align: left;
  // height: 100vh;
  .content{
      margin-top: 20px;
      .list{
          width: 92%;
          margin: 0 auto 10px;
          height: 250px;
          border-radius: 10px;
          background-color: #fff;
          overflow: hidden;
          .list-info{
              position: relative;
              height: 160px;
              color: #fff;
              .list-info-img{
                  width: 100%;
                  height: 160px;
                  background-size: 100% 100%;
                  position: absolute;
                  top: 0;
              }
              .list-info-name{
                  position: absolute;
                  bottom: 35px;
                  left: 15px;
                  font-size: 18px;
              }
              .distance{
                  position: absolute;
                  bottom: 10px;
                  left: 15px;
                  display: flex;
                  align-items: center;
                  font-size: 16px;
                  img{
                      width: 15px;
                      height: 15px;
                      margin-right: 5px;
                  }
              }
          }
          .list-place{
              display: flex;
              align-items: center;
              font-size: 16px;
              color: #000;
              margin-top: 20px;
              margin-left: 15px;
              img{
                  width: 15px;
                  height: 15px;
                  margin-right: 5px;
              }
          }
          .list-price{
              width: 92%;
              margin: 0 auto;
              font-size: 16px;
              color: #fa3223;
              display: flex;
              align-items: center;
              justify-content: space-between;
              .booking-btn{
                  background-color: #2098f6;
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
