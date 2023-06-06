<template>
  <div class="partner-list mb-xl text-nowrap overflow-hidden">
      <div class="partner-list-row overflow-auto scrollbar-hidden">
        <span v-for="i in partnersCount" :key="i">
          <img
            class="partner-logo"
            :src="`https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise${i}.png?raw=true`"
            :alt="'合作企業' + i"
            width="160"
            height="40"
          />
        </span>
      </div>
      <div class="partner-list-row overflow-auto scrollbar-hidden">
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise7.png?raw=true"
          alt="合作企業7"
          width="160"
          height="40"
        />
        <span v-for="i in 2" :key="i">
          <img
            class="partner-logo"
            :src="`https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise${
              i + partnersCount + 1
            }.png?raw=true`"
            :alt="`合作企業${i + partnersCount + 1}`"
            width="160"
            height="40"
          />
        </span>
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise5.png?raw=true"
          alt="合作企業5"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise11.png?raw=true"
          alt="合作企業11"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise12.png?raw=true"
          alt="合作企業12"
          width="160"
          height="40"
        />
        <img
          class="partner-logo"
          src="https://github.com/hexschool/2022-web-layout-training/blob/main/2023web-camp/enterprise7.png?raw=true"
          alt="合作企業7"
          width="160"
          height="40"
        />
      </div>
    </div>
</template>


<script>
export default{
  data(){
    return {
      partnersCount: 6,
    }
  }
}

</script>

<style lang="scss">
.partner-list {
  position: relative;
  text-align: left;
  @include pad {
    text-align: center;
  }
  
}


.first .partner-list-row{
  &:first-child{
    animation: marquee1 10s  linear infinite;
  }
  &:last-child{
    animation: marquee1 13s  linear infinite;
  }
}

.second .partner-list-row{
  &:first-child{
    animation: marquee2 10s linear infinite;
  }
  &:last-child{
    animation: marquee2 13s linear infinite;
  }
}

.partner-list-row{
  &:first-child{

    &::before {
      content: '';
      background: linear-gradient(to right, rgba(0,0,0,1), rgba(0,0,0,0.5), rgba(0,0,0,0.2), rgba(0,0,0,0));
      width: 6rem;
      height: 2.5rem;
      position: absolute;
      left: -1px;
    }
    &::after {
      content: '';
      background: linear-gradient(to left, rgba(0,0,0,1), rgba(0,0,0,0.5), rgba(0,0,0,0.2), rgba(0,0,0,0));
      width: 6rem;
      height: 2.5rem;
      position: absolute;
      right: -1px;
    }
  }
  &:last-child{
    &::before {
      content: '';
      background: linear-gradient(to right, rgba(0,0,0,1), rgba(0,0,0,0.8), rgba(0,0,0,0));
      width: 5rem;
      height: 3rem;
      position: absolute;
      left: -1px;
      bottom: calc(1px + 1.5rem)
    }
    &::after {
      content: '';
      background: linear-gradient(to left, rgba(0,0,0,1), rgba(0,0,0,0.5), rgba(0,0,0,0.2), rgba(0,0,0,0));
      width: 5rem;
      height: 3rem;
      position: absolute;
      right: -1px;
      bottom: calc(1px + 1.5rem)
    }
  }
}

@keyframes marquee1{
  0% {
    transform: translateX(100%);
  }
  100%{
    transform: translateX(-100%);
  }
}

@keyframes marquee2{
  0% {
    transform: translateX(0%);
  }
  100% {
    transform: translateX(-200%);
  }
}

.partner-logo {
  height: 40px;
  width: auto;
  margin: 0 1rem 1.5rem;
}

</style>