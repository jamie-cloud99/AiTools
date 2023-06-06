<template>
  <div class="bg-white text-black rounded-5">
    <div class="container py-xl">
      <h3 class="display-3 fw-bold mb-5">這些超酷的應用，都來自 AI工具王</h3>
      <div class="form-floating mb-4">
        <input
          type="search"
          class="form-control bg-light border-0 rounded-4 px-5"
          name="formId1"
          id="formId1"
          placeholder="搜尋"
          v-model="searchWords"
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
                  <button type="button" class="dropdown-item" @click="filterTools(item, filter.select)" :class="{active: filtersSelected.some(value => value.filter===item && value.type === filter.select) }">{{ item }}</button>
                </li>
                <li v-show="filter.id === 1" class="split-line border-bottom border-black-20 rounded-0"></li>
              </ul>
            </li>
          </ul>
        </div>

        <ul class="d-none d-md-flex align-items-center overflow-auto scrollbar-hidden">
          <li class="mx-1" v-for="item in applicationsBox.type" :key="item">
            <button
              class="btn btn-white text-nowrap"
              :class="{ active: applicationsBox.typeSelected === item }"
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

      <ul class="d-flex d-md-none overflow-auto scrollbar-hidden mb-5">
        <li class="mx-1" v-for="item in applicationsBox.type" :key="item">
          <button
            class="btn btn-white text-nowrap"
            :class="{ active: applicationsBox.typeSelected === item }"
          >
            {{ item }}
          </button>
        </li>
    </ul> 

      <div class="card-list overflow-hidden mb-4">
        <ul class="row gy-3">
          <li class="col-md-6 col-lg-4" v-for="app in searchTools" :key="app.id">
            <div class="card overflow-hidden h-100">
              <div class="overflow-hidden">
                <img
                  class="card-img-top d-block"
                  :src="app.imageUrl"
                  :alt="app.title"
                  width="416"
                  height="312"
                />
              </div>
              <div class="card-body">
                <h4 class="h5 fw-bold mb-2">{{ app.title }}</h4>
                <p class="text-black-80">{{ app.description }}</p>
              </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p class="fw-bold">AI 模型</p>
                  <p class="ms-auto">{{ app.model }}</p>
                </li>
                <li class="list-group-item d-flex justify-content-between py-3">
                  <p>{{ `#${app.type}` }}</p>
                  <a :href="app.link" target="_blank"><ShareIcon></ShareIcon></a>
                </li>
              </ul>
            </div>
          </li>
        </ul>
      </div>
      <PaginationComponent :pagination="tempPagination" @change_page="changePage"></PaginationComponent>
    </div>
  </div>
</template>

<script>
import SearchIcon from 'vue-material-design-icons/Magnify.vue'
import FilterIcon from 'vue-material-design-icons/Filter.vue'
import ShareIcon from 'vue-material-design-icons/ShareVariant.vue'
import PaginationComponent from './PaginationComponent.vue'

export default {
  components:{
    SearchIcon,
    FilterIcon,
    ShareIcon,
    PaginationComponent
  },
  data() {
    return {
      filters: [
        {
          id: 1,
          select: 'AI 模型',
          options: ['所有模型', 'gpt3.5']
        },
        {
          id: 2,
          select: '類型',
          options: ['全部', '問答服務', '虛擬客服', '生活應用', '程式知識', '翻譯助手', '行銷文案']
        }
      ],
      sort: ['由新到舊', '由舊到新'],
      filtersSelected: [],
      isFromNew: true,
      tempApplicationsBox: {
        apps: [{
          title: ''
        }]
      },
      applicationsBox: {
        type: ['全部', '問答服務', '虛擬客服', '生活應用', '程式知識', '翻譯助手', '行銷文案'],
        typeSelected: '全部',
        modelSelected: '全部',
        apps: []
      },
      pagination: { 
        current_page: 1, 
        total_pages: 1, 
        has_next: true,
        has_pre: false
      },
      tempPagination: {},
      searchWords: ''
    }
  },
  methods: {
    sortTools(isFromNew) {
      this.isFromNew = isFromNew
      isFromNew ? this.tempApplicationsBox.apps.sort((a,b) => b.create_time - a.create_time) : this.tempApplicationsBox.apps.sort((a,b) => a.create_time - b.create_time)
    },
    filterTools(filter, type) {
      // 多選filters  toggle
      const newFilter = { filter, type }
      if (this.filtersSelected.some(value=> value.type === type && value.filter === filter)) {
        const index = this.filtersSelected.indexOf(newFilter)
        this.filtersSelected.splice(index, 1)


        if (type === '類型') {
          this.applicationsBox.typeSelected = '全部'
        } else {
          this.applicationsBox.modelSelected = '全部'
        }

      } else if (this.filtersSelected.some(value=> value.type.includes(type))) {
        const index = this.filtersSelected.findIndex(value=> value.type.includes(type))
        this.filtersSelected.splice(index, 1)
        this.filtersSelected.push(newFilter)

        if(type === '類型'){
          this.applicationsBox.typeSelected = filter
        } else {
          this.applicationsBox.modelSelected = filter
        }

      } else {
        this.filtersSelected.push(newFilter)

        if(type === '類型'){
          this.applicationsBox.typeSelected = filter
        } else {
          this.applicationsBox.modelSelected = filter
        }
      }

      this.applicationsBox.typeSelected = this.applicationsBox.typeSelected.replace('所有類型', '全部')
      this.applicationsBox.modelSelected = this.applicationsBox.modelSelected.replace('所有模型', '全部')

      if (this.filtersSelected.length === 0) {
        this.applicationsBox.typeSelected = '全部'
        this.applicationsBox.modelSelected = '全部'
      }

      this.showTool(this.applicationsBox)
    },
    showTool(applicationsBox){
      this.tempApplicationsBox.apps = [...applicationsBox.apps]
      // [], [m, c]
    },
    async fetchTotalTools(){
      const total_pages = await this.fetchTools()
      for(let i=1; i<=total_pages; i++){
          const tempApiUrl = `${import.meta.env.VITE_API}?page=${i}`
          try {
            const res = await this.axios.get(tempApiUrl)
            const apps = res.data.ai_works.data
            this.applicationsBox.apps.push(...apps)
          } catch (error) {
            console.error(error)
          }
        }
      this.tempPagination = this.pagination  
    },
    async fetchTools(page=1){
      const apiUrl = `${import.meta.env.VITE_API}?page=${page}`
      try {
        const res = await this.axios.get(apiUrl)
        this.tempApplicationsBox.apps = res.data.ai_works.data
        this.pagination = res.data.ai_works.page
        this.showTool(this.tempApplicationsBox)
        return res.data.ai_works.page.total_pages
      } catch (error) {
        console.error(error)
      }
    },
    paginate(apps, perPage=6, curPage=1){
      const totalPages = Math.ceil(apps.length / perPage)

      if(curPage > totalPages){
        curPage = totalPages
      }

      const minData = (curPage - 1) * perPage + 1
      const maxData = curPage * perPage


      const newAry = []
      apps.forEach((value, i) => {
        const num = i + 1
        if(num>=minData && num<=maxData) {
          newAry.push(value)
        }
      });

      const page = {
        current_page: curPage,
        total_pages: totalPages,
        has_next: curPage > 1,
        has_pre: curPage < totalPages
      }

      this.tempPagination = page
    },

    changePage(page){
      this.tempPagination.current_page = page
      this.fetchTools(page)
    }
  },
  computed: {
    searchTools(){
      const query = this.searchWords
      return this.tempApplicationsBox.apps.filter(app => app.title.includes(query))
      
    }
  },
  created() {
    this.fetchTotalTools()
  }
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

.split-line {
  margin: 0.75rem 0 0.25rem;
}

</style>
