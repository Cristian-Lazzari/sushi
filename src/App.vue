<script >
  
  import AppNav from './components/AppNav.vue'


  export default {
  components:{  AppNav }
  }
</script>

<template>

  <div class="container">
    <AppNav class="nav" />
    <router-view class="page"></router-view>
  </div>
 

  
</template>

<style lang="scss">
@use './assets/styles/general.scss' as *;
.page::-webkit-scrollbar{
  width: 10px;
}
.page::-webkit-scrollbar-thumb {
  border-radius: 20px;
  background: $c-header;
}
.page::-webkit-scrollbar-thumb:hover {
  border-radius: 20px;
  background-color: $c-nav-link;
  border: 2px solid $c-header;
    
}
body{
  background-color: $c-bg;
}
.nav{
  overflow: hidden;
}
.container{
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding: 0;
  overflow: hidden;
}
.page{
    // position: fixed;
    // top: 0;
    // right: 0;
    width: 100vw;
    padding: 0 2rem 30vh;
    overflow: auto;
    height: calc(100% - 230px);
    margin-top: 230px;
    padding-bottom: 50vh;
  }
  
  
  @media (max-width: 1300px) {
    .page{
      width: 100%;
      height: calc(100% - 125px);

  }
  
}


body::-webkit-scrollbar{
  width: 10px;
}
body::-webkit-scrollbar-thumb {
  border-radius: 20px;
  background: $c-header;
}
body::-webkit-scrollbar-thumb:hover {
  border-radius: 20px;
  background-color: $c-nav-link;
  border: 2px solid $c-header;
    
}

</style>
