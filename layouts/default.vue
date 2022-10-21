<template>
    <div class="layout grid relative ">
        <Sidebar/>
        <div>
          <Nuxt class="layout-content"/>
        </div>
    </div>
  </template>
  <script>
  import Sidebar from '@/components/UI/Sidebar.vue'
  export default {
    components:{
        Sidebar
    }
  }
  </script>
  <style scoped lang="scss">
    .layout{
      grid-template-columns: 0% 100%;
      @media(min-width: 850px){
        grid-template-columns: 20% 80%;
      }
    }
  </style>