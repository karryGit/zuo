<template>
    <div>
      <div class="mask"></div>
    </div>
</template>
<script>
    export default {
        name: 'post'
    }
</script>


<style scoped>
  .mask {
    position: fixed;
    height: 100%;
    width: 100%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, .8);
    z-index: 6000;
  }






</style>
