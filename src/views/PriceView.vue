<template>
  <div class="container">
    <Navigation></Navigation>
    <div class="banner">
      <div class="row">
        <div class="col-md-6">
          <h2 class="display-2 fw-bolder mb-4">用多少，<br />付多少。</h2>
        </div>
      </div>
      <div class="row justify-content-end mb-xl">
        <div class="col-md-6">
          <p class="h1 fw-bold">我們相信，最靈活的取用機制，才能最大化的幫助你業務的推動。</p>
        </div>
      </div>

      <div class="animation-group d-flex overflow-hidden mb-xl">
        <GrassAnimation></GrassAnimation>
      </div>
    </div>

    <div class="card-list overflow-hidden mb-xl">
        <h3 class="fw-bold mb-lg">定價</h3>
        <ul class="row gy-3">
          <li class="col-md-6" v-for="plan in priceingPlans" :key="plan.id">
            <div class="card text-white bg-black border-light h-100">
              <div class="card-body pb-lg">
                <h4 class="h3 fw-bold mb-3">{{ plan.name }}</h4>
                <ul class="list-disc ms-4">
                  <li v-for="item in plan.info" :key="item" class="text-light">{{ item }}</li>
                </ul>
              </div>
              <div class="card-footer d-flex justify-content-between border-top border-light">
                <p class="fw-bold">
                  {{ `NT$${plan.price}` }}<span class="fw-normal text-black-60">／1k tokens</span>
                </p>
                <p>
                  開始使用
                  <CallMadeIcon :size="16" class="ms-2"></CallMadeIcon>
                </p>
              </div>
            </div>
          </li>
        </ul>
      </div>

      <div class="row mb-xl">
        <div class="col-md-4">
          <h3 class="fw-bold mb-5">使用規範</h3>
        </div>
        <div class="col md-8">
          <ul class="list-group rounded-0">
            <li v-for="rule in rules" :key="rule.id" class="border-bottom border-light mb-3">
              <h4 class="h1 fw-bold mb-4">{{ rule.title }}</h4>
              <p class="mb-4">{{ rule.content }}</p>
            </li>
          </ul>
        </div>
      </div>
  </div>

  <ApiList></ApiList>

  <div class="container pt-xl">
    <div class="pb-xl">
      <div class="row">
        <div class="col-md-4">
          <h3 class="fw-bold mb-5">常見問題</h3>
        </div>
        <div class="col-md-8">
          <div class="accordion rounded-4 " id="faqAccordion">
            <div class="accordion-item rounded-4 overflow-hidden mb-3" :class="{active: isQuestionSelected(item.id)}" v-for="item in faq" :key="item.id">
              <h4 class="accordion-header" :id="`heading${item.id}`">
                <button
                  class="accordion-button"
                  type="button"
                  data-bs-toggle="collapse"
                  :data-bs-target="`#collapse${item.id}`"
                  @click.prevent="toggleFaq(item.id)"
                >
                  <PlusIcon class="me-2" 
                  v-show="!isQuestionSelected(item.id)"></PlusIcon>
                  <MinusIcon class="me-2" v-show="isQuestionSelected(item.id)"></MinusIcon>
                  {{ item.question }}
                </button>
              </h4>
              <div
                :id="`collapse${item.id}`"
                class="accordion-collapse collapse"
                data-bs-parent="#faqAccordion"
              >
                <div class="accordion-body">
                  {{ item.answer }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <FooterComponent></FooterComponent>
    <ScrollToTop></ScrollToTop>
  </div>
</template>

<script>
import Navigation from '../components/NavigationComponent.vue'
import ApiList from '../components/ApiList.vue'
import FooterComponent from '../components/FooterComponent.vue'
import GrassAnimation from '../components/GrassAnimation.vue'
import ScrollToTop from '../components/ScrollToTop.vue'

import CallMadeIcon from 'vue-material-design-icons/CallMade.vue'
import PlusIcon from 'vue-material-design-icons/Plus.vue'
import MinusIcon from 'vue-material-design-icons/Minus.vue'

export default {
  components: {
    Navigation,
    ApiList,
    FooterComponent,
    CallMadeIcon,
    PlusIcon,
    MinusIcon,
    GrassAnimation,
    ScrollToTop
  },
  data() {
    return {
      priceingPlans: [
        {
          id: 1,
          name: '琪琪',
          info: ['初級', '速度最快'],
          price: 5
        },
        {
          id: 2,
          name: '昊昊',
          info: ['中級'],
          price: 5
        },
        {
          id: 3,
          name: '卡卡',
          info: ['高級'],
          price: 5
        },
        {
          id: 4,
          name: '杰杰',
          info: ['最高級', '資料最完善'],
          price: 5
        }
      ],
      rules: [
        {
          id: 1,
          title: '守法',
          content: '請遵守相關的法規和政策，不得進行任何違法違規的活動。'
        },
        {
          id: 2,
          title: '資訊安全',
          content: '請務必保護好自己的帳號和密碼，不得將其透露給他人。'
        },
        {
          id: 3,
          title: '守密',
          content: '需對使用過程中產生的數據負責，不得擅自泄露數據。'
        }
      ],
      faq: [
        {
          id: 1,
          question: '如何選擇適合的AI模型？',
          answer:
            '選擇適合的 AI 模型需要考慮您的應用場景、需要解決的問題、可用的資源以及預算等因素。可以通過對比不同模型的性能、準確率、速度等指標，以及與其他用戶的評價與反饋，來選擇最適合的模型。'
        },
        {
          id: 2,
          question: '租用模型的費用是如何計算的？',
          answer:
            '租用模型的費用通常會根據模型的性能和使用時間等因素進行計算。具體而言，模型的性能可以根據其精度、速度、暫用資源等指標來評估；而使用時間可以根據租用時間的長短來計算，通常會按小時、天或月來計算。綜合考慮這些因素，系統會自動算出對應的租用費用。'
        },
        {
          id: 3,
          question: '如何進行付款？',
          answer: '付款方式可以通過網站上提供的線上支付平台進行支付。具體而言，您可以選擇信用卡、銀行轉帳電子錢包等不同的支付方式進行支付。在支付前，您需要先登錄網站並選擇適合的租用方案，系統會自動計算出對應的租用欸用和支付金額，然後您可以選擇適合的支付方式進行支付。完成支付後，系統會自動向您提供相應的服務。'
        },
        {
          id: 4,
          question: '租用模型的期限是多久？',
          answer: '租用模型的期限可以根據您的需求進行設置，通常可以選擇幾個小時、幾天或幾個月等不同的時間段。'
        },
        {
          id: 5,
          question: '如果在使用過程中遇到問題，應該怎麼處理？',
          answer: '如果在使用過程中遇到問題，您可以聯繫客服或技術支持人員進行諮詢或報告問題。您也可以通過網站上的幫助中心或社區論壇尋找相關的解決方案和回答。'
        }
      ],
      questionSelectedId: null
    }
  },
  methods: {
    toggleFaq(id) {
      if(this.isQuestionSelected(id)){
        this.questionSelectedId = null
      } else{
        this.questionSelectedId = id
      }
    },
    isQuestionSelected(id) {
    return this.questionSelectedId === id;
  }
  }
}
</script>
