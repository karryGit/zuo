<template>
  <div>
    <div id="backTop" v-show="isBack">
      <a href="#"><img src="../../assets/images/返回顶部.png"/></a>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'backTop',
    data() {
      return {
        scroll: '',
        isBack: false
      }
    },
    methods: {
      menu() {
        var _this = this;
        document.onmousewheel = function  (e) {
          var e = e ||window.event;

          //1.滚动条滚动的距离
          this.scroll = document.body.scrollTop;

          //2.窗口的可视宽高
          var winHeigth = document.documentElement.clientHeight;

          //3.整体页面的高度
          var pageHeight = document.documentElement.scrollHeight;
          if (e.wheelDelta > 0) {

            if ((winHeigth + this.scroll) / pageHeight > 0.5){
              _this.isBack = false;
              console.log('上')
            }
          }else{
            //判断是否到达底部90%
            if ((winHeigth + this.scroll) / pageHeight > 0.5) {
              console.log('下')
              _this.isBack = true;
            }
          }
        }


      }
    },
    mounted() {
      window.addEventListener('scroll', this.menu)
    }
  }
</script>

<style scoped>
  #backTop {
    position: fixed;
    right: 10%;
    top: 80%;
    width: 40px;
    height: 40px;
  }

  #backTop img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate3D(-50%, -50%, 0);
    width: 100%;
    height: 100%;
    object-fit: cover;
  }


</style>
