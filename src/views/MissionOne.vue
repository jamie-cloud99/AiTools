<template>
  <div class="bg-white text-black rounded-5">
    <div class="container py-xl">
      <div class="card-list overflow-hidden mb-4">
        <div class="row gy-3">
          <div class="col-md-6 col-lg-4" v-for="api in applicationsBox.apis" :key="api.id">
            <div class="card overflow-hidden h-100">
              <div class="overflow-hidden">
                <img
                  class="card-img-top"
                  :src="api.imgUrl"
                  :alt="api.title"
                  width="416"
                  height="312"
                />
              </div>
              <div class="card-body">
                <h4 class="h5 fw-bold mb-2">{{ api.title }}</h4>
                <p class="text-black-80">{{ api.description }}</p>
              </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p class="fw-bold">AI 模型</p>
                  <p class="ms-auto">{{ api.model }}</p>
                </li>
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p>{{ `#${api.category}` }}</p>
                  <a href="#">
                    <ShareIcon></ShareIcon>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ShareIcon from 'vue-material-design-icons/ShareVariant.vue'

export default {
  components:{
      ShareIcon
    },
  data() {
    return {
      applicationsBox: {
        category: ['全部', '聊天', '影像辨識', '翻譯', '行銷', '客服', '生產力'],
        seletedCategory: '全部',
        apis: [
          {
            id: 1,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool1.png?raw=true',
            title: 'Chatbot Builder',
            description: '建立智能化的聊天機器人，解答常見問題、提供客戶支援、收集反饋等。',
            model: '卡卡',
            category: '聊天'
          },
          {
            id: 2,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool2.png?raw=true',
            title: 'Image Recognition Platform',
            description: '專業的圖像識別平台，識別圖像、分類、標記等。',
            model: '杰杰',
            category: '影像辨識'
          },
          {
            id: 3,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool3.png?raw=true',
            title: 'Language Translation API',
            description: '專業的語言翻譯 API，實現文本翻譯功能，支援多種格式的文本。',
            model: '琪琪',
            category: '翻譯'
          },
          {
            id: 4,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool4.png?raw=true',
            title: 'Sentiment Analysis API',
            description:
              '自動識別文本中的情感傾向，包括正向、負向和中性等。適用於情感分析、社交媒體監控、市場調查等。',
            model: '昊昊',
            category: '行銷'
          },
          {
            id: 5,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool5.png?raw=true',
            title: 'Fraud Detection Platform',
            description: '預防詐騙活動，適用於銀行、金融、電商等。',
            model: '卡卡',
            category: '客服'
          },
          {
            id: 6,
            imgUrl:
              'https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/tool6.png?raw=true',
            title: 'Voice Assistant SDK',
            description:
              '通過語音控制應用程式、設備，實現多種功能，例如播放音樂、查詢天氣、發送信息等。',
            model: '杰杰',
            category: '生產力'
          }
        ]
      },
      pagination: {
        totalPages: 5,
        currentPage: 1
      }
    }
  }
}
</script>

<style lang="scss">
.pages {
  justify-content: end;
}

.page {
  .page-link {
    padding: 0.35rem 0.75rem;
    border-radius: 0.75rem;
  }
}
</style>
