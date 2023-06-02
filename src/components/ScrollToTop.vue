<template>
    <button class="position-fixed top-button" @click.prevent="scrollToTop"
      >
      <ArrowUpIcon class="" :size="16"></ArrowUpIcon>
    </button>

</template>

<script>
import ArrowUpIcon from 'vue-material-design-icons/ArrowUp.vue'

export default {
  components:{
    ArrowUpIcon
  },
  methods:{
    scrollToTop(){
      window.scrollTo({top:0, behavior: 'smooth'})
    }
  }
}

</script>


<style lang="scss">
.top-button{
  bottom: 5.5rem;
  right: 0;

  text-align: center;
  padding: 0.5rem 0.75rem;
  border-radius: 1.5rem;
  transition: all 0.4s;

  @include pad{
    bottom: 1rem;
    right: 4rem;
  }

  &:hover{
    &::before{
    content: 'Back to Top';
    padding-right: 0.5rem;
  
  }
  }

}


</style>