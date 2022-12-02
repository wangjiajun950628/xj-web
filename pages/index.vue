<style scoped lang="scss">
  @import "assets/index/index";
</style>
<template>
  <div class="xj-index">
    <v-btn class="particles-button" @click="testClick">Send</v-btn>
  </div>
</template>

<script>
  import anime from 'animejs'
  export default {
    name: 'IndexPage',
    head: {
      title: '首页'
    },
    mounted() {
    },
    methods: {
      testClick() {
      }
    }
  }
</script>

