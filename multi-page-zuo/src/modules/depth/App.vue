<template>
  <div>
    <MyNav></MyNav>
    <MyDepth></MyDepth>
  </div>
</template>

<script>
  import MyNav from '../../components/nav/Nav';
  import MyDepth from '../../components/depth/depth';
  export default {
    name: 'depth',
    components: {
      MyDepth,
      MyNav
    }
  }
</script>

<style scoped>

</style>
