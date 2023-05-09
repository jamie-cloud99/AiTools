<template>
  <div class="container">
    <Navigation></Navigation>
  </div>

  <ApiList></ApiList>

  <div class="container pt-xl">

    <FooterComponent></FooterComponent>
  </div>
</template>


<script>
import Navigation from '../components/NavigationComponent.vue';
import ApiList from '../components/ApiList.vue';
import FooterComponent from '../components/FooterComponent.vue';

export default{
  components:{
    Navigation,
    ApiList,
    FooterComponent
  },
  data(){
    return{

    }
  }

}
</script>