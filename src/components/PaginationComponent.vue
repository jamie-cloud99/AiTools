<template>
  <nav>
    <ul class="d-flex pages">
      <li
        class="page"
        v-for="i in pagination.total_pages"
        :key="i"
        :class="{ active: pagination.current_page === String(i) }"
      >
        <a href="#" class="page-link border-0 fs-sm" @click.prevent="$emit('change_page', i)">
          <span>{{ i }}</span>
        </a>
      </li>
      <li class="page">
        <a href="#" class="page-link border-0 fs-sm">
          <ChevronRightIcon :size="16"></ChevronRightIcon>
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
