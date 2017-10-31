<template>
  <div>
    <header id="depth-container">
      <!--推荐阅读-->
      <div class="depth-body">
        <h3 class="read">推荐阅读</h3>
        <div class="imgWrap">
          <img src="../../assets/pic2.jpg"/>
          <div class="textWrap">
            <div class="img-one">
              拒绝性冷淡 | 从韦斯●安德森的电影里得到的家居配色灵感
            </div>
            <p class="text-one">如果你也受够了黑白灰的MUJI风.</p>
          </div>
          <div class="hengxian"></div>
          <div class="text-footer clear_float">
            <a href="" class="kind">
              <span>●</span>
              <span>&nbsp;视觉</span>
            </a>
            <a href="" class="dateline"><span>06月23日18:44</span></a>
          </div>
        </div>
      </div>
      <!--更多文章-->
      <div class="more-body">
        <h3 class="more">更多文章</h3>
        <div class="more-content">
          <!--图片-->
          <div class="img-two">
            <img src="../../assets/pic2.jpg"/>
          </div>
          <!--文本内容-->
          <div class="text-two">
            <a href="">
              <span>这个感性的双鱼座国家,不只有最画风清奇的球迷,还有这四个划时代好物</span>
            </a>
          </div>
          <!--底部时间部分-->
          <div class="footer-time-wrap clear_float">
            <div class="title-name float-left">
              <a href="">
                <span>zuo先生</span>
              </a>
            </div>
            <div class="title-time float-right">
              <a href="">
                <span>07月30日23:56</span>
              </a>
            </div>
          </div>

        </div>
      </div>

    </header>
  </div>
</template>
<script>
  export default {
    name: 'depth'
  }

</script>

<style scoped>
  @import "../../common/style/marx.min.css";
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
  .footer-time-wrap{
    width: 190px;
    position: relative;
    left: 0;
    top: 91%;
    height: 40px;
  }
  .title-time a{
    font-size: 14px;
    text-decoration: none;
    color: #A4ABB0;
  }
  .title-name a{
    text-decoration: none;
    color: #262721;
   font-weight: 200;
  }
  .text-two{
    font-size: 15px;
    width: 190px;
    position: absolute;
    bottom: 25%;
    text-align: left;
  }
  .text-two a{
    text-decoration: none;
    color: #3A230C;
    font-weight: 200;
  }

  #depth-container {
    margin-top: 70px;
    width: 100%;
  }

  .depth-body {
    width: 960px;
    margin: 0 auto;
  }

  .more-body {
    width: 960px;
    margin: 20px auto;
  }

  .more {
    text-align: center;
  }

  .read {
    text-align: center;
    width: 960px;
    margin-bottom: 30px;
  }

  .more-content {
    border-radius: 5px;
    position: relative;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 220px;
    height: 300px;
  }

  .img-two {
    position: absolute;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    width: 100%;
    height: 50%;
    background-color: #b3d4fc;
  }
  .img-two img{
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    width: 100%;
    height: 100%;
  }

  .imgWrap {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    border-radius: 5px;
    width: 300px;
    height: 450px;
  }

  .imgWrap img {
    border-radius: 5px;
    position: absolute;
    width: 100%;
    height: 100%;
  }

  .img-one {
    font-size: 18px;
    font-weight: 500;
    color: white;
    width: 280px;
  }

  .textWrap {
    text-align: left;
    position: absolute;
    bottom: 25%;
  }

  .text-one {
    margin-top: 20px;
    font-size: 16px;
    color: #E4D6D6;
    width: 280px;
  }

  .hengxian {
    position: absolute;
    left: 5%;
    bottom: 14%;
    width: 90%;
    height: 1px;
    background-color: #C3C5CA;
  }

  .text-footer {
    width: 90%;
    position: relative;
    top: 91%;
    height: 40px;
  }

  .kind {
    float: left;
  }

  .kind span:nth-child(1) {
    color: yellow;
  }

  .kind span:nth-child(2) {
    font-size: 14px;
    color: white;
  }

  .dateline {
    font-size: 14px;
    color: white;
    float: right;
  }


</style>
