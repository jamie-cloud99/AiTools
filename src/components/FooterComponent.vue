<template>
  <footer>
      <div
        class="d-flex justify-content-between align-item-start border-bottom border-light pb-5 mb-5"
      >
        <div class="display-4 fw-bold">
          <RouterLink :to="{name: 'home'}" >首頁</RouterLink>
          <RouterLink :to="{name: 'price'}">定價</RouterLink>
        </div>
        <a href="#" class="logo"
          ><img class="logo-img" :src="logo.imgUrl" :alt="logo.name" width="245" height="40"
        /></a>
      </div>
      <div class="d-flex mb-5 mb-md-3">
        <p class="me-md-5">AI工具王 ©2023</p>
        <div class="d-none d-md-flex">
          <a class="link-light px-3 ms-4" href="#" @click.prevent>Facebook</a>
          <a class="link-light px-3" href="#" @click.prevent>Twitter</a>
          <a class="link-light px-3" href="#" @click.prevent>Instagram</a>
        </div>
        <a class="ms-auto" @click.prevent="scrollToTop"
          >Back to Top
          <ArrowUpIcon class="ms-2" :size="16"></ArrowUpIcon>
        </a>
      </div>
      <div class="d-flex d-md-none flex-wrap mb-4">
        <a class="link-light ps-0 pe-3 px-md-3" href="#" @click.prevent>Facebook</a>
        <a class="link-light px-3" href="#" @click.prevent>Twitter</a>
        <a class="link-light px-3" href="#" @click.prevent>Instagram</a>
      </div>
    </footer>

</template>

<script>
import ArrowUpIcon from 'vue-material-design-icons/ArrowUp.vue'

export default {
  components:{
    ArrowUpIcon
  },
  data(){
    return{
      logo: {
        name: 'AI工具王',
        imgUrl:
          'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/logo.png'
      },
    }
  },
  methods:{
    scrollToTop(){
      window.scrollTo({top:0, behavior: 'smooth'})
    }
  }

}
</script>

<style lang="scss">
.logo-img{
  height: 1.5rem;
  width: auto;
  @include pad{
    height: 2.5rem;
  }
}
</style>

