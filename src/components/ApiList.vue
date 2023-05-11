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
           <SearchIcon :size="16"></SearchIcon>
          </span>
          請輸入搜尋關鍵字
        </label>
      </div>

      <div class="d-flex justify-content-between align-items-center mb-3 mb-md-4">
        <div class="dropdown">
          <button
            type="button"
            class="btn btn-outline-light dropdown-toggle text-black px-4 py-3 me-md-2"
            data-bs-toggle="dropdown"
            data-bs-auto-close="false"
          >
            篩選
            <FilterIcon :size="16" class="ms-2"></FilterIcon>
          </button>
          <ul class="dropdown-menu rounded-4 shadow pb-3" @click.stop>
            <li class="mt-3" v-for="filter in filters" :key="filter.id">
              <p class="fs-xs fw-bold text-black-60 px-3 my-2">{{ filter.select }}</p>
              <ul class="list-group">
                <li class="list-item" v-for="item in filter.options" :key="item">
                  <button type="button" class="dropdown-item" @click="filterTools(item, filter.select)" :class="{active: filtersSelected.some(value => value.filter===item && value.category === filter.select)}">{{ item }}</button>
                </li>
                <li v-show="filter.id === 1" class="split-line border-bottom border-black-20 rounded-0"></li>
              </ul>
            </li>
          </ul>
        </div>

        <ul class="d-none d-md-flex align-items-center overflow-auto">
          <li class="mx-1" v-for="item in applicationsBox.category" :key="item">
            <button
              class="btn btn-white text-nowrap"
              :class="{ active: applicationsBox.categorySelected === item }"
            >
              {{ item }}
            </button>
          </li>
        </ul>

        <div class="dropdown">
          <button
            v-if="isFromNew"
            type="button"
            class="btn btn-outline-light dropdown-toggle form-select text-black ps-4 pe-5 py-3 me-md-2"
            data-bs-toggle="dropdown"
          >
            {{ sort[0] }}
          </button>
          <button
            v-else
            type="button"
            class="btn btn-outline-light dropdown-toggle form-select text-black ps-4 pe-5 py-3 me-md-2"
            data-bs-toggle="dropdown"
          >
            {{ sort[1] }}
          </button>
          <ul class="dropdown-menu rounded-4 overflow-hidden">
            <li>
              <button
                type="button"
                class="btn rounded-0 dropdown-item"
                @click="sortTools(true)"
                :class="{ active: isFromNew }"
              >
                {{ sort[0] }}
              </button>
            </li>
            <li>
              <button
                type="button"
                class="btn rounded-0 dropdown-item"
                @click="sortTools(false)"
                :class="{ active: !isFromNew }"
              >
                {{ sort[1] }}
              </button>
            </li>
          </ul>
        </div>
      </div>

      <ul class="d-flex d-md-none overflow-auto mb-5">
        <li class="mx-1" v-for="item in applicationsBox.category" :key="item">
          <button
            class="btn btn-white text-nowrap"
            :class="{ active: applicationsBox.categorySelected === item }"
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
              <ChevronRightIcon :size="16"></ChevronRightIcon>
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import SearchIcon from 'vue-material-design-icons/Magnify.vue'
import FilterIcon from 'vue-material-design-icons/Filter.vue'
import ShareIcon from 'vue-material-design-icons/ShareVariant.vue'
import ChevronRightIcon from 'vue-material-design-icons/ChevronRight.vue'

export default {
  components:{
    SearchIcon,
    FilterIcon,
    ShareIcon,
    ChevronRightIcon
  },
  data() {
    return {
      filters: [
        {
          id: 1,
          select: 'AI 模型',
          options: ['所有模型', '卡卡', '杰杰', '琪琪', '昊昊']
        },
        {
          id: 2,
          select: '類型',
          options: ['所有類型', '聊天', '影像辨識', '翻譯', '行銷', '客服', '生產力']
        }
      ],
      sort: ['由新到舊', '由舊到新'],
      filtersSelected: [],
      isFromNew: true,
      applicationsBox: {
        category: ['全部', '聊天', '影像辨識', '翻譯', '行銷', '客服', '生產力'],
        categorySelected: '全部',
        modelSelected: '全部',
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
  },
  methods: {
    sortTools(isFromNew) {
      this.isFromNew = isFromNew
    },
    filterTools(filter, category) {
      // 多選filters  toggle
      const newFilter = { filter, category }
      if (this.filtersSelected.some(value=> value.category === category && value.filter === filter)) {
        const index = this.filtersSelected.indexOf(newFilter)
        this.filtersSelected.splice(index, 1)

        console.log(1)
        if (category === '類型') {
          this.applicationsBox.categorySelected = '全部'
        } else {
          this.applicationsBox.modelSelected = '全部'
        }

      } else if (this.filtersSelected.some(value=> value.category.includes(category))) {
        const index = this.filtersSelected.findIndex(value=> value.category.includes(category))
        this.filtersSelected.splice(index, 1)
        this.filtersSelected.push(newFilter)

        console.log(2)
        if(category === '類型'){
          this.applicationsBox.categorySelected = filter
        } else {
          this.applicationsBox.modelSelected = filter
        }

      } else {
        this.filtersSelected.push(newFilter)

        console.log(3)
        console.log(category, filter)
        if(category === '類型'){
          this.applicationsBox.categorySelected = filter
        } else {
          this.applicationsBox.modelSelected = filter
        }
      }

      this.applicationsBox.categorySelected = this.applicationsBox.categorySelected.replace('所有類型', '全部')
      this.applicationsBox.modelSelected = this.applicationsBox.modelSelected.replace('所有模型', '全部')

      if (this.filtersSelected.length === 0) {
        this.applicationsBox.categorySelected = '全部'
        this.applicationsBox.modelSelected = '全部'
      }
    }
  },
  created() {}
}
</script>

<style lang="scss">
.dropdown-menu {
  min-width: 15rem;
}

.dropdown-toggle {
  &::after {
    display: none;
  }
}

.pages {
  justify-content: end;
}

.page {
  .page-link {
    padding: 0.35rem 0.75rem;
    border-radius: 0.75rem;
  }
}

.split-line {
  margin: 0.75rem 0 0.25rem;
}
</style>
