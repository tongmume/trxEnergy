<template>
  <!-- <van-nav-bar :title="$t($route.meta.title as string)" :left-arrow="!tabbarVisible" @click-left="goBack" />
  <div class="main-page" :class="{ tabbar: tabbarVisible, border: showBorder }">
    <RouterView v-slot="{ Component }" v-if="$route.meta.keepAlive">
      <keep-alive>
        <component :is="Component" :key="$route.path" />
      </keep-alive>
    </RouterView>
    <RouterView v-if="!$route.meta.keepAlive" :key="$route.path" />
  </div>
  <nut-tabbar unactive-color="#364636" active-color="#1989fa" bottom v-model="activeTab" v-show="tabbarVisible" @tab-switch="tabSwitch">
    <nut-tabbar-item v-for="item in tabItem" :key="item.key" :tab-title="$t(`tabbar.${item.key}`)" :icon="item.icon" />
  </nut-tabbar> -->
  <div class="self-navbar">
    <div class="navbox">
      <img  class="img-menu" :src="menuImg"/>
      <img  class="img-logo" :src="logoImg"/>
    </div>
  </div>
  <div class="gonggao-box">
    <img class="gonggao-img" :src="gonggaoImg"/>
    <text class="gonggao-txt">尊敬的卖家：波场stake2.0已生效，授权权限需要立....</text>
  </div>
  <div class="wallet-box">
    <text class="wallet-num">TALy13AV6qCj5UmYwn1vUYHxGPBBWAAAAA</text>
    <div class="wallet-content">
      <div class="wallet-content-text">
        <text>余额：123</text>
        <text>能量：123</text>
        <text>带宽：123</text>
      </div>
      <img class="wallet-img" :src="walletImg"/>
    </div>
  </div>
</template>

<script lang="ts" setup name="BasicLayoutPage">
  import { ref, watch } from 'vue' 
  import { useRouter } from 'vue-router';
  import { Home, Horizontal, My, Location } from '@nutui/icons-vue';
  import menuImg from '/@/static/menu.png'
  import logoImg from '/@/static/logo.png'
  import moneyImg from '/@/static/money.png'
  import shopcartImg from '/@/static/shopcart.png'
  import gonggaoImg from '/@/static/gonggao.png'
  import walletImg from '/@/static/wallet.png'

  const tabItem = [
    { key: 'home', icon: Home },
    { key: 'list', icon: Horizontal },
    { key: 'member', icon: My },
    { key: 'demo', icon: Location },
  ];

  const router = useRouter();

  const activeTab = ref(0);

  const tabbarVisible = ref(true);

  const showBorder = ref(true);

  watch(
    () => router,
    () => {
      const judgeRoute = tabItem.some((item) => item.key === router.currentRoute.value.path.replace('/', ''));
      activeTab.value = tabItem.findIndex((item) => item.key === router.currentRoute.value.path.replace('/', ''));
      tabbarVisible.value = judgeRoute;
      showBorder.value = judgeRoute;
    },
    { deep: true, immediate: true },
  );

  const tabSwitch = (_item, index) => {
    switch (index) {
      case 0:
        router.push('/home');
        break;
      case 1:
        router.push('/list');
        break;
      case 2:
        router.push('/member');
        break;
      case 3:
        router.push('/demo');
        break;
    }
    activeTab.value = index;
  };

  const goBack = () => {
    router.go(-1);
  };
</script>

<style scoped lang="scss">
  .nut-navbar {
    margin-bottom: 0;
  }

  .main-page {
    box-sizing: border-box;
    height: calc(100vh - 92px);
    overflow-y: scroll;
    overflow-x: hidden;
  }

  .tabbar {
    height: calc(100vh - 92px);
    padding-bottom: 100px;
  }

  .border {
    padding-left: 30px;
    padding-right: 30px;
  }

  .self-navbar{
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 85px;
    background-color: #35BDB3;
  }

  .navbox{
    margin-top: 25px; 
    width: 100%; 
    height: 60px; 
    display: flex; 
    flex-direction: row;
    align-items: center;
    padding-left: 19px;
  }

  .gonggao-box{
    width: 710px;
    height: 75px;
    display: flex;
    flex-direction: row;
    align-items: center;
    background-color: #F1FBF9;
    margin-left: 20px;
    margin-top: 24px;
  }

  .img-menu{
    width: 28px; 
    height: 20px;
  }

  .img-logo{
    width: 150px; 
    height: 25px; 
    margin-left: 250px;
  }

  .gonggao-img{
    width: 32px;
    height: 32px; 
    margin-left: 20px;
  }

  .gonggao-txt{
    font-size: 24px; 
    color: #333333; 
    margin-left: 24px;
  }

  .wallet-box{
    width: 710px;
    height: 270px;
    background-color: #35BDB3;
    border-radius: 8px;
    display: flex;
    margin-top: 23px;
    margin-left: 20px;
    flex-direction: column;
  }

  .wallet-num{
    font-size: 26px;
    color: #FFFFFF;
    margin-top: 21px;
    margin-left: 30px;
    flex: 1;
  }

  .wallet-content{
    width: 702px;
    height: 186px;
    align-self: center;
    margin-bottom: 3px;
    background-color: #FFFFFF;
    border-radius: 8px;
    padding-bottom: 20px;
    display: flex;
    flex-direction: row;
  }

  .wallet-content-text{
    width: 100%;
    display: flex;
    flex-direction: column;
    align-self: flex-end;
    margin-left: 42px;
  }

  .wallet-img{
    width: 54px;
    height: 54px;
    margin-right: 24px;
    align-self: flex-end;
    align-items: flex-end;
  }
</style>
