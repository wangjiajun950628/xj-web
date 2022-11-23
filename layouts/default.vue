<template>
  <v-app style="background-color: #F5F5F5;">
    <!--  头部  -->
    <v-app-bar class="xj-app" fixed app color="#212121" height="55">
      <canvas slot="img" id="canvas"></canvas>
      <!--   pc端导航布局   -->
      <div class="xj-pc-nav-box d-none d-sm-flex">
        <div class="xj-pc-logo">logo</div>
        <div class="xj-pc-nav-right">
          <ul class="xj-pc-ul">
            <li
              :class="['xj-pc-li hvr-underline-from-center',navValue === item.id ? 'xj-nav-activity' : '']"
              v-for="(item, index) in navList"
              :key="index"
              @click="toPage(item)"
            >
              <router-link :to="item.url">{{ item.title }}</router-link>
            </li>
          </ul>
        </div>
      </div>
      <!--   移动端导航布局   -->
      <div class="xj-mobile-nav-box d-flex d-sm-none">
        <div class="xj-mobile-logo">logo</div>
        <div class="xj-mobile-drawer">
          <v-icon @click.stop="rightDrawer =! rightDrawer" v-ripple>mdi-menu</v-icon>
        </div>
      </div>
    </v-app-bar>
    <!--  内容  -->
    <v-main>
      <div class="xj-main">
        <Nuxt/>

      </div>
    </v-main>
    <!--  页脚  -->
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
    <!--  移动端导航  -->
    <v-navigation-drawer v-model="rightDrawer" right temporary fixed>
      <div class="xj-mobile-nav">
        <!--        <div style="padding: 20px 0">卡片信息</div> hvr-rectangle-in-->
        <ul class="xj-mobile-ul">
          <li
            :class="['xj-mobile-li', navValue === item.id ? 'xj-nav-activity' : '']"
            @click="toPage(item)"
            v-for="(item, index) in navList"
            :key="index"
          >
            <router-link :to="item.url">{{ item.title }}</router-link>
          </li>
        </ul>
      </div>
    </v-navigation-drawer>
  </v-app>
</template>

<script>
  export default {
    name: 'DefaultLayout',
    data() {
      return {
        fixed: false,
        rightDrawer: false,
        navList: [
          { title: '首页', url: '/', icon: '', id: 0 },
          { title: '每时每刻', url: 'daily', icon: '', id: 1 },
          { title: '关于我', url: 'about_me', icon: '', id: 2 }
        ],
        navValue: ''
      }
    },
    head: {
      script: [
        // { src: require('~/plugins/svg')}
      ]
    },
    mounted() {
      this.initPage()
    },
    methods: {
      // 初始化页面数据
      initPage() {
        this.initNavStatus()
      },
      // 跳转页面
      toPage(e) {
        this.navValue = e.id
      },
      // 初始化导航状态
      initNavStatus() {
        switch (this.$route.name) {
          case 'index':
            this.navValue = 0
            break;
          case 'daily':
            this.navValue = 1
            break;
          case 'about_me':
            this.navValue = 2
            break;
          default:
            this.navValue = 0
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  @import "assets/layout";
  @import "~hover.css";
</style>
