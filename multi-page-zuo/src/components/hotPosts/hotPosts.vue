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
      <!--评论部分-->
      <main id="comment-container" v-for="(post,index) in posts">
        <!--评论头部-->
        <header class="comment-header">
          <header class="comment-header-left clear_float">
            <img class="comment-header-c" src="../../assets/hotPostsImg/c.png"/>
            <div class="comment-header-left-img float-left">
              <img :src="post.owner.avatar" alt="">
            </div>
            <div class="comment-header-left-text float-left">
              <a href="#">{{post.owner.username}}</a>
            </div>
            <div class="comment-header-dot float-right">
              <img src="../../assets/hotPostsImg/Dot.png"/>
            </div>
            <div class="comment-header-share float-right">
              <img src="../../assets/hotPostsImg/share.png"/>
            </div>
            <span class="approve float-right">{{post.likeCount}}个赞同</span>
            <div class="comment-header-right-round float-right">
              <img src="../../assets/hotPostsImg/round.png"/>
            </div>
          </header>
        </header>
        <!--评论图片-->
        <div class="comment-image-overlay">
          <img :src="post.postImage.url" alt="">
            <div  class="mask"></div>
          <a href="" class="feed-halo" :style="{left:(post.haloCenterRatio.width_ratio*100)-10+'%'
          ,top:(post.haloCenterRatio.height_ratio * 100)-10 + '%'}">
            <div class="like-tip goods">
              <span class="animated-pop"></span>
                <div class="hide">
                  <div class="like-tip-big">赞同</div>
                  <div class="like-tip-small">这个态度</div>
                </div>
            </div>
          </a>
        </div>
        <!--底部评论-->
        <div class="comment-content">
          <div class="comment-footer">
            {{post.postDescription}}
          </div>
          <div class="comment-footer-space">
            <a href="" class="circle">
              ●<span>&nbsp;空间</span>
            </a>
            <a href="">●
              <span>
                &nbsp;零售空间
              </span>
            </a>
            <a href="">●
              <span>&nbsp;Herman Miller</span>
            </a>
          </div>
          <div class="more-info">
            <div class="more-info-comment">
              <img src="../../assets/hotPostsImg/info.png"/>
              <span>{{post.commentedCount}}条评论</span>
              <span>更多评论...</span>
            </div>
            <ul class="comment-list">
              <li class="comment-item">
                <div class="comment-item-name">
                  <a href="">{{post.comments[0].author.username}}</a>
                  <span>-&nbsp;</span>
                  <span v-html="post.comments[0].text"></span>
                </div>
                <div class="coment-item-time clear_float">
                  <span class="coment-item-time-before">{{post.comments[0].timeAgo}}</span>
                  <span class="coment-item-time-reply">
                   <a href="">回复</a>
                     <span>点亮</span>
                     <span><strong>{{post.comments[0].likeNumber}}</strong></span>
                  <img src="../../assets/hotPostsImg/bulb.png"/>
                 </span>
                </div>
              </li>
              <li class="comment-item" v-if="post.comments.length== 2">
                <div class="comment-item-name" v-html="post.comments[1].author.username">
                  <!--<a href="" v-html=""></a>-->
                  <span>-&nbsp;</span>
                  <span v-html="post.comments[1].text">{{post.comments[1].text}}</span>
                </div>
                <div class="coment-item-time clear_float">
                  <span class="coment-item-time-before">{{post.comments[1].timeAgo}}</span>
                  <span class="coment-item-time-reply">
                   <a href="">回复</a>
                     <span>点亮</span>
                     <span><strong>{{post.comments[1].likeNumber}}</strong></span>
                  <img src="../../assets/hotPostsImg/bulb.png"/>
                 </span>
                </div>
              </li>
            </ul>
          </div>
          <!--写下你的评论-->
          <div class="add-comment">
            <div class="add-body">
              <div class="input-wrap">
                  <textarea placeholder="写下你的评论..." class="comment-text"
                            style="margin-top: 0px; margin-bottom: 0px; height: 100px;">

                  </textarea>
              </div>
              <div class="add-comment-actions clear_float">
                <a href="" class="cancel-new-comment float-left" @click="cancelClick">取消</a>
                <a href="" class="post-new-comment float-right">评论</a>
              </div>
            </div>
          </div>
        </div>
      </main>
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
        arrayJson: [],
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
      },
      cancelClick(){

      }
    },
    mounted() {
      var _this = this;
      axios.get('api/web_hot_posts').then(function (response) {
        console.log(response)
        let array = response.data.posts;
        for (var i = 0; i < array.length; i++) {
          _this.posts.push(array[i]);
          _this.arrayJson.push(array[i].comments);
          console.log(array[i].comments);
        }
      }).catch(function (err) {
        console.log(err);
      })
    }
  }
</script>

<style scoped>
  @import '../../../node_modules/vue2-animate/dist/vue2-animate.min.css';
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
    border: 3px solid #ececec;
    height: 708px;
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

  #comment-container {
    width: 600px;
    margin: 15px 0;
    border-radius: 5px;
    position: relative;
    background-color: #fff;
    z-index: 450;
  }

  .comment-header {
    margin-left: 10px;
    margin-top: 10px;
    width: 100%;
    height: 45px;
  }

  .comment-header-left {
    position: relative;
    top: 5px;
  }

  .comment-header-c {
    position: absolute;
    left: -10px;
    top: 0;
    width: 20px;
    height: 20px;
  }

  .comment-header-left-img {
    width: 50px;
    height: 50px;
  }

  .comment-header-left-img img {
    border-radius: 50%;
  }

  .comment-header-left-text {
    margin-left: 10px;
    margin-top: 12px;
  }

  .comment-header-dot {
    margin-top: 10px;
    margin-right: 15px;
    width: 25px;
    height: 25px;
  }

  .comment-header-share {
    width: 22px;
    height: 22px;
    margin-right: 15px;
    margin-top: 10px;
  }

  .approve {
    margin-top: 10px;
    margin-right: 20px;
    color: #9B9C9D;
  }

  .comment-header-right-round {
    margin-right: 10px;
    margin-top: 10px;
    width: 22px;
    height: 22px;
  }

  .comment-image-overlay {
    margin-bottom: -20%;
    position: relative;
    margin-left: -17px;
    width: 600px;
  }
  .comment-image-overlay:hover .hide{
    opacity: 1;
  }
  .comment-image-overlay:hover .mask{

    opacity: 1;
  }
  .comment-image-overlay:hover .goods{
    border: 4px solid #1fd7e2;
  }

  .feed-halo {
    position: absolute;
    left: 0;
    top: 0;
    color: white;
  }
  .hide{
    transition:all 1s;
    opacity: 0;
  }

  .mask {
    opacity: 0;
    transition: all 1s;
    position: absolute;
    height: 99%;
    width: 100%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, .4);
  }

  .like-tip {
    z-index: 1000;
    width: 120px;
    height: 120px;
    text-align: center;
    opacity: 1;
    visibility: visible;
  }

  .goods {
    width: 130px;
    height: 130px;
    border: 2px solid #1fd7e2;
    border-radius: 50%;
    background-color: rgba(31, 217, 255, .2);
  }

  .like-tip-big {
    position: absolute;
    left: 17%;
    top: 20px;
    font-size: 38px;
  }

  .like-tip-small {
    position: absolute;
    left: 18%;
    top: 70px;
    font-size: 20px;
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

  .comment-content {
    margin-top: 120px
  }

  .comment-footer {
    line-height: 22px;
    padding: 0 25px 18px;
    color: #595c5d;
  }

  .comment-footer-space .circle {
    color: #00B8E9;
  }

  .comment-footer-space {
    margin-left: 25px;
    width: 520px;
    padding-bottom: 15px;
    border-bottom: 1px solid #ECECEC;
  }

  .comment-footer-space span {
    color: #A6A7A7;
  }

  .comment-footer-space a {
    color: #A6A7A7;
    margin-left: 5px;
    text-decoration: none;
  }

  .comment-footer-space span:hover {
    color: black;
  }

  .more-info {
    margin-left: 25px;
    width: 520px;
    padding-bottom: 15px;
    border-bottom: 1px solid #ECECEC;
  }

  .more-info-comment img {
    vertical-align: middle;
    margin-left: 25px;
    width: 20px;
    height: 20px;
  }

  .more-info-comment span {
    margin-left: 5px;
    height: 100%;
    vertical-align: middle;
    line-height: 30px;
    color: #A2A3A3;
  }

  .more-info-comment {
    margin-top: 10px;
    margin-left: -20px;
    margin-bottom: 20px;
  }

  .comment-list li {
    margin-left: -15px;
    list-style: none;
  }

  .comment-item {
    padding-left: 5px;
    margin-top: -5px;
    line-height: 30px;
    margin-left: 20px;
    height: 70px;
    width: 500px;
  }

  .comment-list {
    padding-left: 0;
  }

  .comment-item-name {
    margin-left: 15px;
  }

  .coment-item-time {
    margin-left: 18px;
  }

  .comment-list li:hover {
    border-radius: 5px;
    width: 520px;
    height: 70px;
    background-color: rgb(247, 247, 247);
  }

  .comment-item-name a {

    font-size: 15px;
    font-weight: 500;
  }

  .comment-item-name span {

    font-size: 15px;
  }

  .coment-item-time span {
    color: #C9C9C9;
  }

  .coment-item-time {
    display: inline-block;
  }

  .coment-item-time-before {
    font-size: 14px;
  }

  .coment-item-time-reply {
    margin-left: 300px;
  }

  .coment-item-time-reply span {
    color: #A1A2A3;
    margin-left: 5px;
    line-height: 30px;
    height: 100%;
    vertical-align: middle;
    font-size: 14px;
  }

  .coment-item-time-reply a {
    color: #A1A2A3;
    line-height: 35px;
    font-size: 14px;
  }

  .coment-item-time-reply img {
    vertical-align: middle;
    width: 15px;
    height: 15px;
  }

  .add-comment {
    margin-top: 10px;
    margin-left: 20px;
  }

  .comment-text {
    outline: none;
    border: none;
    width: 520px;
    height: 100px;
    resize: vertical;
  }

  .add-comment-actions {
    margin-left: 10px;
    width: 500px;
    height: 30px;
  }


</style>
