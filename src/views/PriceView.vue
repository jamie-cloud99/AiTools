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
      <div class="mb-xl">
        <span v-for="i in 3" :key="i">
          <img
            class="banner-animation grass-icon"
            src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/deco.png"
            alt="grass"
            width="160"
            height="160"
          />
        </span>
      </div>
    </div>

    <div class="card-list overflow-hidden mb-xl">
        <h3 class="fw-bold mb-lg">定價</h3>
        <div class="row gy-3">
          <div class="col-md-6" v-for="plan in priceingPlans" :key="plan.id">
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
          </div>
        </div>
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
            <div class="accordion-item rounded-4 border border-light overflow-hidden mb-3" v-for="item in faq" :key="item.id">
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
  </div>
</template>

<script>
import Navigation from '../components/NavigationComponent.vue'
import ApiList from '../components/ApiList.vue'
import FooterComponent from '../components/FooterComponent.vue'

import CallMadeIcon from 'vue-material-design-icons/CallMade.vue'
import PlusIcon from 'vue-material-design-icons/PLus.vue'
import MinusIcon from 'vue-material-design-icons/Minus.vue'

export default {
  components: {
    Navigation,
    ApiList,
    FooterComponent,
    CallMadeIcon,
    PlusIcon,
    MinusIcon
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
            '選擇適合的AI模型需要考慮問題的性質、數據的特徵、計算資源和預算等因素。明確定義問題，評估數據資源和可用計算資源，了解模型的複雜性和架構，考慮使用預訓練模型和開源庫，並進行模型的評估和測試。綜合這些因素，選擇最適合的模型能夠提高準確度和效能，並解決您的問題。'
        },
        {
          id: 2,
          question: '租用模型的費用是如何計算的？',
          answer:
            '琪琪模型：每小時 $10 美元，每月 $100 美元。昊昊模型：每小時 $20 美元，每月 $200 美元。卡卡模型：每小時 $50 美元，每月 $500 美元。杰杰模型：客制方案需洽詢顧問。'
        },
        {
          id: 3,
          question: '如何進行付款？',
          answer: '我們有單次支付與每月訂閱兩種方式，可使用信用卡或線上轉帳付款。'
        },
        {
          id: 4,
          question: '租用模型的期限是多久？',
          answer: '我們以一個月為單位向您收費。'
        },
        {
          id: 5,
          question: '如果在使用過程中遇到問題，應該怎麼處理？',
          answer: '請洽客服電話：02-23453456，或諮詢粉絲頁線上客服。'
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
