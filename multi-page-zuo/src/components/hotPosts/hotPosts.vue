<template>
  <div>
    <section id="hotPosts_container">
      <div class="bar-wrap clear_float">
        <div class="bar-left float-left" @click="jiaoClick">
          <div class="bar-left-dian">
            <img src="../../assets/hotPostsImg/dian-b.png"/>
          </div>
          <span class="bar-text">全部</span>
          <div class="bar-left-jiao">
            <img src="../../assets/hotPostsImg/down.png"/>
          </div>
        </div>
        <div class="bar-right float-right">
          <a href="#" class="good" @click="goodClick">
            <img :src="goodImg"/>
            <span>好设计</span>
          </a>
          <a href="#" class="bad" @click="badClick">
            <img :src="badImg"/>
            <span>坏设计</span>
          </a>
        </div>
        <ul v-show="isShow" class="dropdown-menu">
          <span class="dropdown-arrow"></span>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <img src="../../assets/hotPostsImg/dian-b副本.png"/>
              <span class="bar-all">全部</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round1">●</span>
              <span class="bar-all">日用</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">公共</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">关爱</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">家具</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">时尚</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">美食</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">数码</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">视觉</span>
            </a>
          </li>
          <li class="dropdown-li">
            <a href="" class="dropdown-li-a">
              <span class="round">●</span>
              <span class="bar-all">空间</span>
            </a>
          </li>
        </ul>
      </div>
      <div class="zanAll">
        <div class="zan">
          <span>
                赞
              </span>
          <p class="animated-pop">
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'hotPosts',
    data() {
      return {
        tf: 0,
        tr: 0,
        goodImg: require('../../assets/hotPostsImg/check-box.png'),
        badImg: require('../../assets/hotPostsImg/check-box (1).png'),
        posts: [],
        isShow: false
      }
    },
    methods: {
      goodClick() {
        this.tf++;
        if (this.tf == 1) {
          this.goodImg = require('../../assets/hotPostsImg/check-box_click.png');
        } else if (this.tf == 2) {
          this.goodImg = require('../../assets/hotPostsImg/check-box.png');
          this.tf = 0;
        }
      },
      badClick() {
        this.tr++;
        if (this.tr == 1) {
          this.badImg = require('../../assets/hotPostsImg/check-box_click.png');
        } else if (this.tr == 2) {
          this.badImg = require('../../assets/hotPostsImg/check-box (1).png');
          this.tr = 0;
        }

      },
      jiaoClick() {
        this.isShow = !this.isShow;
      }
    },
    mounted() {
      var _this = this;
      axios.get('api/web_hot_posts').then(function (response) {
        let array = response.data.posts;
        for (var i = 0; i < array.length; i++) {
          _this.posts.push(array[i])
        }
        console.log(response.data.posts)
      }).catch(function (err) {
        console.log(err);
      })
    }
  }
</script>

<style scoped>
  /*浮动左*/
  .float-left {
    float: left;
  }

  /*浮动右*/
  .float-right {
    float: right;
  }

  /*清除浮动必须加到父级元素上*/
  .clear_float::after {
    content: "";
    display: table;
    clear: both;
  }

  #hotPosts_container {
    width: 600px;
    margin-left: 150px;
  }

  .bar-wrap {
    position: relative;
    width: 600px;
    height: 20px;
  }

  .bar-left {
    position: relative;
  }

  .bar-left-dian {
    position: absolute;
    width: 20px;
    height: 20px;
  }

  .bar-text {
    width: 50px;
    position: absolute;
    left: 25px;
  }

  .bar-left-jiao {
    position: absolute;
    top: 1px;
    left: 65px;
    width: 20px;
    height: 20px;
  }

  .bar-right img {
    width: 20px;
    height: 20px;
  }

  .good {
    text-decoration: none;
    width: 20%;
    height: 60px;
    text-align: center;
  }

  .good span {
    color: #959697;
    height: 100%;
    vertical-align: middle;
    line-height: 30px;
  }

  .good img {
    border-radius: 5px;
    vertical-align: middle;
  }

  .bad {
    text-decoration: none;
    width: 20%;
    height: 60px;
    text-align: center;
  }

  .bad span {
    color: #959697;
    height: 100%;
    vertical-align: middle;
    line-height: 30px;
  }

  .bad img {
    border-radius: 5px;
    vertical-align: middle;
  }

  .dropdown-arrow {
    position: absolute;
    width: 13px;
    height: 13px;
    border-left: 1px solid #ccc;
    border-top: 1px solid #ccc;
    border-right: 0;
    border-bottom: 0;
    background-color: #fff;
    -webkit-transform: rotate(45deg);
    transform: rotate(45deg);
    margin-left: -5px;
    top: -6px;
    left: 48px;
  }

  .dropdown-menu {
    height: 704px;
    width: 100px;
    background-color: white;
    position: relative;
    top: 32px;
    min-width: 100px;
    left: -3px;
    padding: 5px 10px;
  }

  .dropdown-menu li {
    margin-top: 10px;
    height: 60px;
    border-bottom: 1px solid #ececec;
    padding: 5px 0;
    list-style: none;
  }

  .dropdown-li-a {
    padding: 15px 10px;
    text-decoration: none;
    color: #a6a7a7;
    font-weight: 500;
    text-align: center;
    border-radius: 4px;
    margin-bottom: 5px;
  }

  .dropdown-menu li a:hover {
    padding: 15px 10px;
    background-color: rgb(245, 245, 245);
  }

  .dropdown-li-a img {
    width: 20px;
    height: 20px;
    vertical-align: middle;
  }

  .dropdown-li-a span:hover {
    color: black;
  }

  .dropdown-li-a span {
    color: #959697;
    height: 100%;
    vertical-align: middle;
    line-height: 40px;
  }

  .dropdown-li a .round {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    color: #0c7cd5;
    margin-right: 10px;
  }

  .dropdown-li a .round1 {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    color: #d5352a;
    margin-right: 10px;
  }

  .zanAll{
    position: relative;
  }
  .zan {
    width: 50px;
    height: 50px;
  }
  .animated-pop {
    border: 1px solid #1fd7e2;
    border-radius: 50%;
    background-color: rgba(31, 217, 255, .2);
    display: block;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    transition: all 1s;
    animation: animatepop 1s infinite
  }

  @keyframes animatepop {
    0% {
      transform: scale(1);
      opacity: 1;
    }
    100% {
      transform: scale(1.5);
      opacity: 0;
    }
  }
  .zan span{
    line-height: 50px;
    margin-left: 15px;
    color: transparent;
  }
  .zan :hover{
   line-height: 50px;
    margin-left: 15px;
    color: black;
  }


</style>
