<template>
  <div>
    <MyNav></MyNav>
    <MySearch></MySearch>
    <MyFooter></MyFooter>
  </div>
</template>

<script>
  import MyNav from '../../components/nav/Nav';
  import MySearch from '../../components/nav/search';
  import MyFooter from '../../components/footer/footer';
  import MyBackTop from '../../components/index/backTop';
  export default {
    name: 'logon',
    components: {
      MyNav,
      MySearch,
      MyFooter
    }
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";

</style>
