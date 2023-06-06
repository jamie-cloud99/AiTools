<template>
  <nav>
    <ul class="d-flex pages">
      <li
        class="page me-1"
        v-for="i in pagination.total_pages"
        :key="i"
        :class="{ active: pagination.current_page === i }"
      >
        <a href="#" class="page-link border-0 fs-sm" @click.prevent="$emit('change_page', i)">
          <span>{{ i }}</span>
        </a>
      </li>
      <li class="page" :class="{ disabled: pagination.current_page === pagination.total_pages }">
        <a href="#" class="page-link border-0 fs-sm px-2" @click.prevent="$emit('change_page', pagination.current_page+1)">
          <ChevronRightIcon :size="14"></ChevronRightIcon>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
import ChevronRightIcon from 'vue-material-design-icons/ChevronRight.vue'

export default {
  components: {
    ChevronRightIcon
  },
  props: ['pagination'],
  emits: ['change_page'],
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
