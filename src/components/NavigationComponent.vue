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
          @click="toggleMenu"
        >
          <MenuIcon v-if="!isOpen"></MenuIcon>
          <CloseIcon v-else></CloseIcon>
        </div>
      </div>
      <div class="collapse navbar-collapse flex-grow-0" id="navbarNav">
        <ul class="d-md-flex text-center" :class="{'menu-list-mb': isOpen}">
          <li class="menu-item">
            <RouterLink class="link-white p-3" :to="{name: 'home'}" >首頁</RouterLink>
          </li>
          <li class="menu-item">
            <RouterLink class="link-white p-3" :to="{name: 'price'}">定價</RouterLink>
          </li>
        </ul>
        <div class="menu-footer-mb" v-show="isOpen">
          <FooterLink></FooterLink>
        </div>        
      </div>
    </nav>

</template>


<script>
import FooterLink from './FooterLink.vue';

import MenuIcon from 'vue-material-design-icons/Menu.vue'
import CloseIcon from 'vue-material-design-icons/Close.vue'

export default {
  components:{
    MenuIcon,
    FooterLink,
    CloseIcon
  },
  data(){
    return{
      logo: {
        name: 'AI工具王',
        imgUrl:
          'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/logo.png'
      },
      isOpen: false
    }
  },
  methods:{
    toggleMenu(){
      this.isOpen = !this.isOpen
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

.menu-list-mb{
  transition: all 1s;
  height: 75vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  .menu-item{
    font-size: 5rem;
    font-weight: bold;
    line-height: 1;
  }
}

.menu-footer-mb{
  @include pad{
    display: none;
  }
}
</style>