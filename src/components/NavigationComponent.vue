<template>
  <nav
      class="d-md-flex navbar-expand-md justify-content-between align-items-center border-bottom border-light py-3 mb-3"
    >
      <div class="d-flex justify-content-between align-items-center">
        <h1>
          <span class="visually-hidden">AI工具王</span>
          <a href="#" class="logo">
            <img class="logo-img" :src="logo.imgUrl" :alt="logo.name" width="245" height="40"
          />
          
        </a>
        </h1>
        <div
          class="d-md-none nav-menu navbar-toggler"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
        >
          <MenuIcon></MenuIcon>
        </div>
      </div>
      <div class="collapse navbar-collapse flex-grow-0" id="navbarNav">
        <ul class="d-md-flex text-center">
          <li class="menu-item">
            <RouterLink class="link-white p-3" :to="{name: 'home'}" >首頁</RouterLink>
          </li>
          <li class="menu-item">
            <RouterLink class="link-white p-3" :to="{name: 'price'}">定價</RouterLink>
          </li>
        </ul>
      </div>
    </nav>

</template>


<script>
import MenuIcon from 'vue-material-design-icons/Menu.vue'

export default {
  components:{
    MenuIcon
  },
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