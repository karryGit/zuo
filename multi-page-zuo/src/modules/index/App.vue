<template>
  <div>
    <MyNav></MyNav>
    <my-index></my-index>
  </div>
</template>
<script>
  import MyIndex from '../../components/index/Index';
  import MyNav from '../../components/nav/Nav';


  export default {
    name: 'index',
    components: {
        MyIndex,
        MyNav
    },
  }
</script>

<style scoped>
@import "../../common/style/marx.min.css";






</style>
