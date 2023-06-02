<template>
  <TransitionGroup name="fade">
    <span v-for="item in grassImages" :key="item.id" v-show="item.isShow">
      <img class="grass-icon" :src="item.imgUrl" alt="grass" width="160" height="160" />
    </span>
  </TransitionGroup>
</template>

<style lang="scss">
.grass-icon{
  height: 117px;
  width: auto;
  @include pad{
    height: 160px;
  }
}

.fade-enter-from{
  opacity: 0;
  transform: translateY(160px);
}

.fade-leave-to{
  opacity: 0;
  transform: translateY(-160px);
}


.fade-enter-active,.fade-leave-active{
  transition: all 1.75s ease;
}
</style>

<script>
export default {
  data() {
    return {
      grassImages: [
        {
          id: 1,
          imgUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/deco.png',
          isShow: false
        },
        {
          id: 2,
          imgUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/deco.png',
          isShow: false
        },
        {
          id: 3,
          imgUrl:
            'https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/2023web-camp/deco.png',
          isShow: false
        }
      ]
    }
  },
  methods:{
    showAnimationSequentially(){
    this.showAnimation(0)
  },
  showAnimation(index){
    if(index<this.grassImages.length){
      this.grassImages[index].isShow = true
      setTimeout(()=>{
        return this.showAnimation(index+1)
      }, 300)
    } else {
      setTimeout(()=>{
        this.hideAnimationSeqentially()
      },1500)
    }
  },
  hideAnimationSeqentially(){
    this.hideAnimation(0)
  },
  hideAnimation(index){
    if(index<this.grassImages.length){
      this.grassImages[index].isShow = false
      setTimeout(()=>{
        return this.hideAnimation(index+1)
      }, 200)
    } else {
      setTimeout(()=>{
        this.showAnimationSequentially()
      },2000)
    }
  }
  },
  mounted(){
    this.showAnimationSequentially()
  }
}
</script>

