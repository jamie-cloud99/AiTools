<template>
  <div class="container">
    <Navigation></Navigation>

    <div class="banner">
      <h2 class="display-2 fw-bolder mb-4">
        透過<br />AI工具王的<br />強大模型<br />讓您的業務更聰明
      </h2>
      <button class="btn btn-outline-light fs-5 fw-bold px-4 py-2 mb-5">
        開始使用
        
      </button>
      <div class="text-end mb-xl">
        <span v-for="i in 3" :key="i">
          <img class="banner-animation grass-icon" src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/deco.png" alt="grass" width="160" height="160"/>
        </span>
      </div>
    </div>

    <div class="row mb-5">
      <h3 class="col-md-4">我們的服務</h3>
      <p class="col-md-8">
        我們相信透過 AI 技術，<br />
        包括圖像識別、自然語言處理和機器翻譯等，讓您更快、更準確地做出決策。
      </p>
    </div>

    <div class="card-list overflow-hidden mb-xl">
      <div class="row gy-3">
        <div class="col-md-4" v-for="feature in features" :key="feature.title">
          <div class="card text-white bg-black border-light h-100">
            <div class="card-body py-lg">
              <img class="icon-lg mb-3" :src="feature.iconUrl" :alt="feature.title" width="80" height="80" />
              <h4 class="h5 fw-bold mb-3">{{ feature.title }}</h4>
              <p>{{ feature.content }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="partners">
      <h2 class="mb-lg">來自合作夥伴</h2>
      <div class="partner-list mb-xl text-nowrap overflow-auto">
        <span v-for="i in partnersCount" :key="i">
          <img
            class="partner-logo"
            :src="`https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise${i}.png?raw=true`"
            :alt="'合作企業' + i"
            width="160"
            height="40"
          />
        </span>
        <br>
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise7.png?raw=true"
          alt="合作企業7"
          width="160"
          height="40"
        />
        <span v-for="i in 2" :key="i">
          <img
            class="partner-logo"
            :src="`https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise${
              i + partnersCount + 1
            }.png?raw=true`"
            :alt="`合作企業${i + partnersCount +1}`"
            width="160"
            height="40"
          />
        </span>
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise5.png?raw=true"
          alt="合作企業5"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise11.png?raw=true"
          alt="合作企業11"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise12.png?raw=true"
          alt="合作企業12"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise7.png?raw=true"
          alt="合作企業7"
          width="160"
          height="40"
        />
      </div>
    </div>

    <div class="card-list mb-xl">
      <div class="row">
        <Swiper class="mySwiper" :pagination="true" :modules="modules" :slides-per-view="slidesPerView">
          <SwiperSlide class="col-md-4" v-for="review in reviews" :key="review.id">
            <div class="card bg-dark text-white h-100">
              <div class="card-body d-flex flex-column">
                <p class="mb-3">
                  <span v-for="i in review.starsCount" :key="i">
                    <img
                      src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/star.png"
                      alt="review stars"
                      width="16"
                      height="16"
                    />
                  </span>
                </p>
                <p class="mb-5">{{ review.content }}</p>
                <div class="d-flex mt-auto">
                  <div class="avatar-img rounded-circle me-3">
                    <img
                      :src="review.customerImgUrl"
                      :alt="review.customerName"
                      width="48"
                      height="48"
                    />
                  </div>
                  <div>
                    <p>{{ review.customerName }}</p>
                    <p>{{ review.companyName }}</p>
                  </div>
                </div>
              </div>
            </div>
          </SwiperSlide>
        </Swiper>
      </div>
    </div>
  </div>

  <ApiList></ApiList>

  <div class="container pt-xl">
    <div class="text-center border-bottom border-light pb-xl mb-5">
      <h3 class="mb-4 fw-bold">現在就來建立屬於你的服務吧</h3>
      <button class="btn btn-outline-light fs-5 fw-bold px-4">開始使用 
        <img class="icon-md align-middle ms-2" src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/call%20made.png" alt="start arrow">
      </button>
    </div>

    <FooterComponent></FooterComponent>
  </div>
</template>

<style lang="scss">

.swiper{
  overflow-x: clip;
  overflow-y: visible;
}

.swiper-slide{
  padding: 0 0.5rem;
}

.swiper-horizontal>.swiper-pagination-bullets{
  bottom: -30px

}

.swiper-pagination-bullet{
  background-color: #ffffffd1;
}

.swiper-pagination-bullet-active{
  background-color: #fff;
}



.grass-icon{
  height: 117px;
  width: auto;
  @include pad{
    height: 160px;
  }
}

.partner-list{
  text-align: left;
  @include pad{
    text-align: center;
  }
}

.partner-logo {
  height: 40px;
  width: auto;
  margin: 0 1rem 1.5rem;
}


</style>

<script>
 // Import Swiper Vue.js components
 import { Swiper, SwiperSlide } from 'swiper/vue';
// Import Swiper styles
import 'swiper/css';
import 'swiper/css/pagination';
// import required modules
import { Pagination } from 'swiper';

import Navigation from '../components/NavigationComponent.vue';
import FooterComponent from '../components/FooterComponent.vue';
import ApiList from '../components/ApiList.vue';

export default {
  components: {
    Swiper,
    SwiperSlide,
    Navigation,
    FooterComponent,
    ApiList
  },

  data() {
    return {
      
      features: [
        {
          iconUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/flash%20on.png',
          title: '快速',
          content: '我們先進的推理基礎設施提供了極短的響應時間，讓你的產品服務不間斷。'
        },
        {
          iconUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/auto%20awesome.png',
          title: '靈活',
          content: '我們的服務可以根據您的需求進行靈活調整，同時還可以滿足不同項目和預算的需求。'
        },
        {
          iconUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/library%20add.png',
          title: '擴充',
          content: '我們的服務支持多種擴充選項，可以滿足您的不斷增長的 AI 需求。'
        }
      ],
      partnersCount: 6,
      reviews: [
        {
          id: 1,
          customerImgUrl:
            'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/avatar3.png?raw=true',
          customerName: '陳小姐',
          companyName: 'ABC科技有限公司',
          starsCount: 5,
          content:
            '非常喜歡 AI工具王 提供的 AI 模型租賃服務，使用起來非常方便，而且效果非常好。對於我們公司的業務來說，這個服務非常重要，因為我們需要大量的數據進行分析和預測，AI工具王 提供的 AI 模型能夠幫助我們節省大量時間和成本，實在是太棒了！'
        },
        {
          id: 2,
          customerImgUrl:
            'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/avatar1.png?raw=true',
          customerName: '劉小姐',
          companyName: 'XYZ 醫療器材有限公司',
          starsCount: 5,
          content:
            '作為一家醫療器材公司，我們非常關注人工智能技術的應用，而 AI工具王 提供的 AI 模型租賃服務為我們帶來了很大的幫助。我們使用 AI工具王 的模型進行醫學影像分析和預測，這些模型非常精確，能夠幫助我們更好地診斷病情，提高治療效果。感謝 AI工具王 團隊的辛勤工作！'
        },
        {
          id: 3,
          customerImgUrl:
            'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/avatar2.png?raw=true',
          customerName: '黃先生',
          companyName: 'EFG 銀行',
          starsCount: 5,
          content:
            '我們銀行一直在尋找能夠幫助我們提高風險控制和客戶服務的解決方案，而 AI工具王 提供的 AI 模型租賃服務正好滿足了我們的需求。我們使用 AI工具王 的模型進行客戶信用評估和詐騙檢測等任務，這些模型非常準確，能夠幫助我們更好地控制風險，提高客戶滿意度。非常感謝 AI工具王 團隊的支持！'
        }
      ],
      
      modules: [Pagination],
      screenWidth: 1000
    }
  },
  computed:{
    slidesPerView(){
      const minPadWidth = 768
      if(this.screenWidth>=minPadWidth){
        return 3
      } else{
        return 1
      }
    } 
 },
 methods: {
  getScreenWidth() {
    this.screenWidth = window.innerWidth
  }
 },
 mounted() {
    this.getScreenWidth()
    window.addEventListener('resize', this.getScreenWidth)
  },
  
}
</script>
