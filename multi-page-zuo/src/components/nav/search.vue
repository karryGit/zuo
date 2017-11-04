<template>
  <div>
    <div class="search-container">
      <!--头部-->
      <div class="search-body">
        <div class="search-title">
          <span>🔍 &nbsp;</span>
          <span> 搜索: {{hrefValue}}</span>
        </div>
        <div class="search-text">
          <a href="" v-for="header in headerArr">
            <span>
              <span :class="{activeClass : header.isTopic}">●</span>
              {{header.content}}</span>
          </a>
        </div>
      </div>
    </div>
    <div class="search-read-body">
      <!--相关深度阅读-->
      <div class="search-read-body-container">
        <h3>相关深度阅读</h3>
        <div class="flex-list">
          <div class="read-one" v-for="pgcs in pgcsArr">
            <a target="_blank" class="pgc-mask" :href="pgcs.origin_url"></a>
            <img :src="pgcs.banner" alt="">
            <div class="read-two">
              <a href="">{{pgcs.title}}</a>
            </div>
            <div class="read-three">
              <p :style="{color:pgcs.sceneTagColor}">{{pgcs.summary}}</p>
            </div>
          </div>
        </div>
      </div>
      <!--相关用户-->
      <div class="search-user-body">
        <h3>相关用户</h3>
        <div class="flex-list">
          <div class="user-one">

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  var href = location.href.split('?');
  export default {
    name: 'search',
    data() {
      return {
        hrefValue: href[1],
        headerArr: [],
        pgcsArr: [],
      }
    },
    methods: {},
    mounted() {
      var _this = this;
      axios.get('api/search?q=' + this.hrefValue).then(function (response) {
        let array = response.data.query.tags
        for (var i = 0; i < array.length; i++) {
          _this.headerArr.push(array[i]);
        }
      });
      axios.get('api/search/articles?q=' + this.hrefValue).then(function (response) {
        let array = response.data.pgcs;
        for (var i = 0; i < array.length; i++) {
          _this.pgcsArr.push(array[i]);
        }
        console.log(_this.pgcsArr)
      });
      axios.get('api/search/users?q=' + this.hrefValue).then(function (response) {

      });
      axios.get('api/search/posts?q=' + this.hrefValue).then(function (response) {

      });
    }

  }
</script>

<style scoped>
  .search-container {
    width: 100%;
    height: 120px;
    background-color: #fdfdfd;
  }

  .search-read-body {
    width: 100%;
    height: 1000px;
    background-color: #F6F6F6;
  }

  .search-read-body-container {
    width: 960px;
    margin: 0 auto;
  }

  .search-user-body {
    width: 960px;
    margin: 0 auto;
  }

  .flex-list {
    display: flex;
    -ms-flex-align: center;
    align-items: center;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    -webkit-box-pack: start;
    -ms-flex-pack: start;
    justify-content: flex-start;
  }

  .read-one {
    position: relative;
    width: 219px;
    height: 180px;
    margin-right: 18px;
    border-radius: 4px;
  }

  .user-one {
    position: relative;
    display: block;
    width: 219px;
    margin-bottom: 18px;
    margin-right: 18px;
    background-color: white;
  }

  .pgc-mask {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .3);
    border-radius: 4px;
  }

  .read-two {
    width: 180px;
    position: absolute;
    left: 5%;
    bottom: 30%;
  }

  .read-three {
    position: absolute;
    left: 5%;
    bottom: 0;
  }

  .read-three p {
    width: 180px;
    height: 20px;
    overflow: hidden;
    font-size: 14px;
  }

  .read-two a {
    text-decoration: none;
    color: white;
  }

  .read-one img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .search-body {
    width: 930px;
    margin: 70px auto;
    height: 100%;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
  }

  .search-user-body {
    padding-top: 30px;
    padding-bottom: 30px;
    text-align: center;
  }

  .search-read-body-container h3 {
    padding-top: 30px;
    padding-bottom: 30px;
    text-align: center;
  }

  .search-text a .activeClass {
    color: #09D8E1;
  }

  .search-text a .errorClass {
    color: #09D8E1;
  }

  .search-title {
    width: 930px;
    margin-bottom: -30px;
  }

  .search-title span {
    padding-left: 8px;
    font-size: 18px;
    font-weight: 500;
    color: #272c2f;
  }

  .search-text a {
    text-decoration: none;
  }

  .search-text span {
    padding-left: 10px;
    color: #A6A7A7;
  }
</style>
