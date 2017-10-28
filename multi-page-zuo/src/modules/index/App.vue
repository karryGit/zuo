<template>
  <div id="all">
    <MyNav></MyNav>
    <my-index></my-index>
    <div id="wrap" class="clear_float">
      <MyHeader id="left"></MyHeader>
      <MyHotTags id="right"></MyHotTags>
    </div>
  </div>
</template>
<script>
  import MyIndex from '../../components/index/Index';
  import MyNav from '../../components/nav/Nav';
  import MyHeader from '../../components/header/header';
  import MyHotTags from '../../components/hotTags/hotTags';
  import MyAttention from '../../components/Attention/Attention';

  export default {
    name: 'index',
    components: {
      MyIndex,
      MyNav,
      MyHeader,
      MyHotTags
    },
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
#all{
  width: 100%;
  background-color: rgb(246, 246, 246);
}
  #wrap {
    width: 86%;
    margin: 0 auto;
  }
  #right {
    margin-top: 4.6%;
    margin-right: 15%;
   float: right;
  }
  #left{
    float: left;
  }
  .clear_float::after{
    content: "";
    display: table;
    clear: both;
  }


</style>
