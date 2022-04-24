<template>
  <Home v-if="active == 0"></Home>
  <My v-if="active == 1"></My>
  <nut-tabbar v-model:visible="active" :bottom="true" unactive-color="#7d7e80" safe-area-inset-bottom active-color="#1989fa">
    <nut-tabbar-item tab-title="首页" icon="home"></nut-tabbar-item>
    <nut-tabbar-item tab-title="我的" icon="my"></nut-tabbar-item>
  </nut-tabbar>
</template>

<script>
import { reactive, toRefs } from 'vue';
import Home from '../home/home.vue'
import My from '../my/my.vue'
export default {
  name: 'Index',
  components: {
    Home,
    My
},
  setup(){
    const state = reactive({
      active: 0
    });
    return {
      ...toRefs(state),
    }
  }
}
</script>

<style lang="scss">
</style>
