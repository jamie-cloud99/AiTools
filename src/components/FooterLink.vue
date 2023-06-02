<template>
  <div class="d-flex flex-group mb-5 mb-md-4 align-items-start">
    <p class="me-md-5 mb-4 mb-md-0">AI工具王 ©2023</p>
    <div class="d-flex">
      <a class="link-light ps-0 pe-3 px-md-3 ms-0 ms-md-4" href="#" @click.prevent>Facebook</a>
      <a class="link-light px-3" href="#" @click.prevent>Twitter</a>
      <a class="link-light px-3" href="#" @click.prevent>Instagram</a>
    </div>
    
  </div>
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
  },
  methods:{
    scrollToTop(){
      window.scrollTo({top:0, behavior: 'smooth'})
    }
  }

}
</script>

<style lang="scss">
.flex-group{
  flex-direction: column;
  @include pad{
    flex-direction: row;
  }
}
</style>