<template>
  <v-app style="background-color: #F5F5F5;">
    <!--  头部  -->
    <v-app-bar class="xj-app" fixed app color="#212121" height="55">
      <!--   pc端导航布局   -->
      <div class="xj-pc-nav-box d-none d-sm-flex">
        <div class="xj-pc-logo">logo</div>
        <div class="xj-pc-nav-right">
          <ul class="xj-pc-ul">
            <li
              :class="['xj-pc-li hvr-underline-from-center',navValue === index ? 'xj-nav-activity' : '']"
              v-for="(item, index) in navList"
              :key="index"
              @click="toPage(index)"
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
          <v-icon @click.stop="rightDrawer = !rightDrawer" v-ripple>mdi-menu</v-icon>
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
        <!--        <div style="padding: 20px 0">卡片信息</div>-->
        <ul class="xj-mobile-ul">
          <li
            :class="['xj-mobile-li hvr-rectangle-in', navValue === index ? 'xj-nav-activity' : '']"
            v-for="(item, index) in navList"
            :key="index"
            @click="toPage(index)"
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
        drawer: false,
        fixed: false,
        rightDrawer: false,
        navList: [
          { title: '首页', url: '/', icon: '' },
          { title: '每时每刻', url: '/', icon: '' },
          { title: '关于我', url: '/', icon: '' }
        ],
        navValue: 0
      }
    },
    head: {
      script: [
        // { src: require('~/plugins/svg')}
      ]
    },
    mounted() {
    },
    methods: {
      toPage(e) {
         this.navValue = e
      }
    }
  }
</script>

<style scoped lang="scss">
  @import "assets/layout";
  @import "~hover.css";
</style>
