<template>
  <div>
    <section id="hot_container">
      <header class="side-title">热门标签</header>
      <button class="btn" v-for="hotTag in hotTags">{{hotTag.content}}</button>
    </section>

  </div>
</template>

<script>
  import axios from 'axios';

  export default {

    name: 'hotTags',
    data() {
      return {
        hotTags: []
      }
    },
    mounted() {
      var _this = this
      axios.get('api/web_hot_tags').then(function (response) {
        var arr = response.data.hot_tags;
        for (var i = 0; i < arr.length; i++) {
          _this.hotTags.push(arr[i])
        }
        console.log(_this.hotTags[0].content)
      })
    }

  }
</script>

<style scoped>
  #hot_container {
    width: 220px;
    position: relative;
  }

  .side-title {

  }

  .btn {
    margin: 5px;
    color: rgb(153, 155, 156);
    padding: 5px;
    background-color: rgb(234, 236, 237);
  }

</style>
