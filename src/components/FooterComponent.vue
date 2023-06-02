<template>
  <footer class="border-top border-white pt-5">
      <div
        class="d-flex footer-flex justify-content-between align-item-start border-bottom border-white pb-5 mb-5"
      >
        <div class="display-4 fw-bold">
          <RouterLink :to="{name: 'home'}" >首頁</RouterLink>
          <RouterLink :to="{name: 'price'}">定價</RouterLink>
        </div>
        <a href="#" class="logo pb-4"
          ><img class="logo-img-md" :src="logo.imgUrl" :alt="logo.name" width="245" height="40"
        /></a>
      </div>
      <FooterLink></FooterLink>
    </footer>

</template>

<script>
import FooterLink from './FooterLink.vue'

export default{
  data(){
    return{
      logo: {
      name: 'AI工具王',
      imgUrl: 'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/logo.png'
    }
    }
  },
  components:{
    FooterLink
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

.logo-img-md{
  height: 2.5rem;
}

.footer-flex{
  flex-direction: column-reverse;
  @include pad{
    flex-direction: row;
  }
}
</style>

