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
              {{header.content}}
            </span>
          </a>
        </div>
      </div>
    </div>
    <div class="search-read-body" v-if="pgcsArr.length!=0">
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
      <div v-if="usersArr.length !=0" class="search-user-body">
        <h3>相关用户</h3>
        <div class="flex-list">
          <div class="user-one" v-for="user in usersArr">
            <!--国产后妈title-->
            <div class="user-title">
              <a href="###" :title="user.nickname" class="float-left">{{user.username}}</a>
              <button class="btnConcern float-right">关注</button>
            </div>
            <!--用户头像-->
            <div class="user-Faces">
              <div class="c">
                <img src="../../assets/images/C.png"/>
              </div>
              <div class="avatar">
                <img :src="user.avatar" alt="">
              </div>
            </div>
            <!--用户发布-->
            <div class="text-info-item">
              <div class="info-count">{{user.all_createposts_count}}</div>
              <div class="info-tip">发布</div>
            </div>
            <!--被赞-->
            <div class="text-info-item-two">
              <div>
                {{user.allLikesCount}}
              </div>
              <div>
                被赞
              </div>
            </div>
          </div>
        </div>
      </div>
      <!--相关ZUO-->
      <div v-if="postsArr.length !=0" class="correlation-zuo">
        <h3>相关ZUO</h3>
        <div class="flex-list">
          <div class="correlation-one" v-for="posts in postsArr">
            <!--来自:title-->
            <div class="correlation-title">
              <span class="correlation-title-span">
                来自
                <a href="###" class="correlation-title-a">{{posts.owner.username}}</a>
              </span>
            </div>
            <!--图片-->
            <div class="correlation-img">
              <img :src="posts.postImage.url" alt="">
            </div>
            <!--footer-->
            <div class="correlation-footer">
              <span :style={color:posts.sceneTag.color}>●</span>
              <a href="">{{posts.sceneTag.name}}</a>
            </div>
            <span class="correlation-footer-span">
                <a href="">●{{posts.tags[0]}}</a>
              </span>
            <!--底部-->
            <div class="correlation-footer-two">
              <div class="correlation-footer-two-img">
                <img src="../../assets/hotPostsImg/round.png"/>
              </div>
            </div>
            <div class="correlation-footer-three">
              <span>{{posts.likeCount}}</span>
            </div>
            <!--信息-->
            <div class="correlation-footer-message">
              <img src="../../assets/images/信息.png"/>
              <span>&nbsp;{{posts.commentedCount}}</span>
            </div>
            <!--分享-->
            <div class="shareImg">
              <img @click="shareClickedY" src="../../assets/images/转发.png"/>
            </div>
          </div>
        </div>
      </div>
    </div>
    <MyShare :pass="isShowShare" @shareClicked="shareClick"></MyShare>
  </div>
</template>

<script>
  import axios from 'axios';
  import MyShare from '../../components/hotPosts/share';

  var href = location.href.split('?');
  export default {
    name: 'search',
    components: {
      MyShare
    },
    data() {
      return {
        hrefValue: href[1],
        headerArr: [],
        pgcsArr: [],
        usersArr: [],
        postsArr: [],
        isShowShare: false
      }
    },
    methods: {
      shareClickedY() {
        this.isShowShare = true;
      },
      //分享事件
      shareClick(value) {
        this.isShowShare = value;
      }
    },
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
      });
      axios.get('api/search/users?q=' + this.hrefValue).then(function (response) {
        let array = response.data.users;
        for (var i = 0; i < array.length; i++) {
          _this.usersArr.push(array[i])
        }
      });
      axios.get('api/search/posts?q=' + this.hrefValue).then(function (response) {
        let array = response.data.posts;
        for (var i = 0; i < array.length; i++) {
          _this.postsArr.push(array[i]);
        }
        console.log(_this.postsArr)
      });
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

  .search-container {
    width: 100%;
    height: 120px;
    background-color: #fdfdfd;
  }

  .search-read-body {
    width: 100%;
    padding-bottom: 30px;
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
    height: 110px;
    border-radius: 5px;
    margin-bottom: 30px;
    margin-right: 18px;
    background-color: white;
  }

  .user-title {
    position: absolute;
    left: 10px;
    top: 8px;
    width: 190px;
    height: 30px;
    border-bottom: 1px solid #ECECEC;
  }

  .user-Faces {
    position: absolute;
    left: 10px;
    top: 50px;
  }

  .c {
    position: absolute;
    z-index: 1;
    width: 18px;
    height: 18px;
  }

  .c img {
    width: 100%;
    height: 100%;
  }

  .avatar {
    width: 50px;
    height: 50px;
    position: absolute;
    left: 8px;
  }

  .text-info-item {
    position: absolute;
    left: 100px;
    bottom: 10px;
  }

  .text-info-item div {
    font-weight: 500;
    color: #A6A7A7;
  }

  .text-info-item-two {
    position: absolute;
    left: 160px;
    bottom: 10px;
  }

  .text-info-item-two div {
    font-weight: 500;
    color: #A6A7A7;
  }

  .avatar img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
  }

  .btnConcern {
    border: none;
    padding: 1px 8px;
    outline: none;
    background-color: #09D8E1;
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

  .search-user-body h3 {
    padding-bottom: 30px;
    text-align: center;
  }

  .correlation-zuo {
    width: 960px;
    margin: 0 auto;

  }

  .correlation-zuo h3 {
    padding-bottom: 30px;
    text-align: center;
  }

  .correlation-one {
    overflow: hidden;
    background-color: #FFFFFF;
    margin-right: 15px;
    margin-top: 15px;
    position: relative;
    border-radius: 5px;
    width: 219px;
    height: 357px;
  }

  .correlation-title {
    position: absolute;
    left: 10px;
    top: 10px;
  }

  .correlation-img {
    width: 217px;
    height: 219px;
    position: absolute;
    top: 12%;
    overflow: hidden;
  }

  .correlation-img {
    width: 217px;
    height: 219px;
  }

  .correlation-img img:hover {
    transition: 0.5s;
    transform: scale(1.2);
  }

  .correlation-title-span {
    color: #A6A7A7;
  }

  .correlation-footer {
    width: 200px;
    height: 30px;
    border-bottom: 1px solid #ECECEC;
    position: absolute;
    left: 10px;
    top: 280px;
  }

  .correlation-footer-span {
    width: 200px;
    position: absolute;
    left: 70px;
    top: 280px;
  }

  .correlation-footer-span a {
    color: #A6A7A7;
  }

  .correlation-footer a {
    color: #A6A7A7;
  }

  .correlation-footer-two {
    position: absolute;
    left: 10px;
    bottom: 12px;
  }

  .correlation-footer-two-img {
    width: 20px;
    height: 20px;
  }

  .correlation-footer-three {
    position: absolute;
    left: 40px;
    top: 324px;
    color: #A6A7A7;
  }

  .correlation-footer-message {
    width: 50px;
    position: absolute;
    left: 80px;
    top: 322px;
  }

  .shareImg {
    position: absolute;
    left: 185px;
    bottom: 4px;
  }

  .shareImg img {
    width: 25px;
    height: 25px;
  }

  .correlation-footer-message img {
    width: 20px;
    height: 20px;
    vertical-align: middle;
  }

  .correlation-footer-message span {
    height: 100%;
    vertical-align: middle;
    line-height: 30px;
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
