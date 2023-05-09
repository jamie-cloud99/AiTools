<template>
  <footer>
      <div
        class="d-flex justify-content-between align-item-start border-bottom border-light pb-5 mb-5"
      >
        <div class="display-4 fw-bold">
          <a href="#">首頁</a>
          <a href="#">定價</a>
        </div>
        <a href="#" class="logo"
          ><img class="logo-img" :src="logo.imgUrl" :alt="logo.name" width="245" height="40"
        /></a>
      </div>
      <div class="d-flex mb-5 mb-md-3">
        <p class="me-md-5">AI工具王 ©2023</p>
        <div class="d-none d-md-flex">
          <a class="link-light px-3 ms-4" href="#">Facebook</a>
          <a class="link-light px-3" href="#">Twitter</a>
          <a class="link-light px-3" href="#">Instagram</a>
        </div>
        <a class="ms-auto" href="#"
          >Back to Top
          <img
            class="icon-sm"
            src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/arrow%20upward.png"
            alt="arrow up"
            width="16"
            height="16"
        /></a>
      </div>
      <div class="d-flex d-md-none flex-wrap mb-4">
        <a class="link-light ps-0 pe-3 px-md-3" href="#">Facebook</a>
        <a class="link-light px-3" href="#">Twitter</a>
        <a class="link-light px-3" href="#">Instagram</a>
      </div>
    </footer>

</template>

<script>

export default {
  data(){
    return{
      logo: {
        name: 'AI工具王',
        imgUrl:
          'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/logo.png'
      },
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

