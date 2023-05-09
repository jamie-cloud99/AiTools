<template>
  <div class="bg-white text-black rounded-5">
    <div class="container py-xl">
      <h3 class="display-3 fw-bold mb-5">這些超酷的應用，都來自 AI工具王</h3>
      <div class="form-floating mb-4">
        <input
          type="text"
          class="form-control bg-light border-0 rounded-4"
          name="formId1"
          id="formId1"
          placeholder="搜尋"
        />
        <label for="formId1" class="text-muted ps-md-4">
          <span class="me-2">
            <img
              class="align-middle"
              src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/icons/search.png"
              alt="search"
              width="16"
              height="16"
            />
          </span>
          請輸入搜尋關鍵字
        </label>
      </div>

      <div class="d-flex justify-content-between align-items-center mb-3 mb-md-4">
        <button class="btn btn-outline-light text-black px-4 py-3 me-md-2" type="button">
          篩選
          <img
            src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/icons/sliders-horizontal.png?raw=true"
            alt="filter"
            width="16"
            height="16"
          />
        </button>
        <ul class="d-none d-md-flex align-items-center overflow-auto">
          <li class="mx-1" v-for="item in applicationsBox.category" :key="item">
            <button
              class="btn btn-white text-nowrap"
              :class="{ active: applicationsBox.seletedCategory === item }"
            >
              {{ item }}
            </button>
          </li>
        </ul>
        <button class="btn btn-outline-light text-black px-4 py-3 me-md-2" type="button">
          由新到舊
          <img
            src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/icons/keyboard%20arrow%20down.png?raw=true"
            alt="arrow down"
            width="16"
            height="16"
          />
        </button>
      </div>
      <ul class="d-flex d-md-none overflow-auto mb-5">
          <li class="mx-1" v-for="item in applicationsBox.category" :key="item">
            <button
              class="btn btn-white text-nowrap"
              :class="{ active: applicationsBox.seletedCategory === item }"
            >
              {{ item }}
            </button>
          </li>
        </ul>
      <div class="card-list overflow-hidden mb-4">
        <div class="row gy-3">
          <div class="col-md-6 col-lg-4" v-for="api in applicationsBox.apis" :key="api.id">
            <div class="card overflow-hidden h-100">
              <div class="overflow-hidden">
                <img class="card-img-top" :src="api.imgUrl" :alt="api.title" width="416" height="312"/>
              </div>
              <div class="card-body">
                <h4 class="h5 fw-bold mb-2">{{ api.title }}</h4>
                <p>{{ api.description }}</p>
              </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p class="fw-bold">AI 模型</p>
                  <p class="ms-auto">{{ api.model }}</p>
                </li>
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p>{{ `#${api.category}` }}</p>
                  <a href="#">
                    <img
                      src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/icons/share.png?raw=true"
                      alt="share"
                      width="24"
                      height="24"
                    />
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <nav>
        <ul class="d-flex pages">
          <li
            class="page"
            v-for="i in pagination.totalPages"
            :key="i"
            :class="{ active: pagination.currentPage === i }"
          >
            <a href="#" class="page-link border-0 fs-sm">
              <span class="align-middle">{{ i }}</span>
            </a>
          </li>
          <li class="page">
            <a href="#" class="page-link border-0 fs-sm">
              <img
                class="align-middle"
                src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/icons/keyboard%20arrow%20right.png?raw=true"
                alt="next page"
              />
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>

</template>


<script>
export default{
  data(){
    return{
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
      },
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
