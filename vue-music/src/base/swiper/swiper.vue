<template>
  <div>
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide"><img src="./shouye_nvsheng_washblow_one.png" class="main-img"></div>
        <div class="swiper-slide"><img src="./shouye_nvsheng_washcutblow_two.png" class="main-img"></div>
        <div class="swiper-slide"><img src="./shouye_nvsheng_hairperm_three.png" class="main-img"></div>
        <div class="swiper-slide"><img src="./shouye_nvsheng_hairdye_four.png" class="main-img"></div>
        <div class="swiper-slide"><img src="./shouye_nvsheng_haircare_five.png" class="main-img"></div>
        <div class="swiper-slide"><img src="./shouye_nvsheng_packeage_six.png" class="main-img"></div>
      </div>
    </div>
    <div class="swiper-pagination" id="pagination"></div>
  </div>
</template>

<script>
  import 'swiper/dist/css/swiper.css'
  import Swiper from 'swiper/dist/js/swiper.js'

  export default {
    data () {
      return {
        mySwiper: ''
      }
    },
    created () {
      this._swiper()
    },
    methods: {
      _swiper () {
        this.mySwiper = new Swiper('.swiper-container',{
          slidesPerView: 'auto',
          centeredSlides: !0,
          watchSlidesProgress: !0,
          pagination: '.swiper-pagination',
          paginationClickable: !0,
          paginationBulletRender: function(a, b) {
            switch (a) {
              case 0:
                name = '洗'
                break
              case 1:
                name = '剪'
                break
              case 2:
                name = '烫'
                break
              case 3:
                name = '染'
                break
              case 4:
                name = '护'
                break
              case 5:
                name = '套'
                break
              default:
                name = ''
            }
            return '<span class="' + b + '"><i>' + name + '</i></span>'
          },
          onProgress: function(a) {
            var b, c, d
            for (b = 0; b < a.slides.length; b++) {
              c = a.slides[b],
              d = c.progress,
              scale = 1 - Math.min(Math.abs(.2 * d), 1),
              es = c.style,
              es.opacity = 1 - Math.min(Math.abs(d / 2), 1),
              es.webkitTransform = es.MsTransform = es.msTransform = es.MozTransform = es.OTransform = es.transform = 'translate3d(0px, 0,' + -Math.abs(150 * d) + 'px)'
            }
          },
          onSetTransition: function(a, b) {
            for (let c = 0; c < a.slides.length; c++) {
              let es = a.slides[c].style,
              es.webkitTransitionDuration = es.MsTransitionDuration = es.msTransitionDuration = es.MozTransitionDuration = es.OTransitionDuration = es.transitionDuration = b + 'ms'
            }
          }
        })
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  *
    margin: 0
    padding: 0
  html
    height: 100%
  body
    height: 100%
    background: #000
    background-size: 100% 100%
  #header img
    width: 100%
  .swiper-container
    width: 100%
    -webkit-perspective: 1200px
    -moz-perspective: 1200px
    -ms-perspective: 1200px
    perspective: 1200px
  .swiper-wrapper
    margin-top: 10px
  .swiper-slide
    width: 80%
    -webkit-transform-style: preserve-3d
    -moz-transform-style: preserve-3d
    -ms-transform-style: preserve-3d
    transform-style: preserve-3d
  .swiper-slide .main-img
    width: 80%
    margin: 0 auto
    display: block
  #pagination
    position: absolute
    bottom: 100px
    width: 100%
  #pagination .swiper-pagination-bullet
    width: 9.5%
    float: left
    margin: 0 0 0 6.15%
    background: 0
    opacity: 1
  .swiper-pagination-bullet i
    background: #41203f
    width: 24px
    height: 24px
    line-height: 24px
    font-size: 12px
    border-radius: 50px
    display: block
    font-style: normal
    text-align: center
    margin: 0 auto
    color: #f5b55c
  .swiper-pagination-bullet-active i
    -webkit-transform: scale(1.5)
    background: #ef0
    background-size: auto 100%
    color: #815d4b
  @media screen and (min-height: 481px)
    .swiper-wrapper
      margin-top:20px
    #pagination
      bottom: 110px
  @media screen and (min-height: 569px)
    .swiper-wrapper
      margin-top:40px
    #pagination
      bottom: 120px
    .swiper-pagination-bullet i
      width: 30px
      height: 30px
      line-height: 30px
      font-size: 15px
  #footer
    position: absolute
    bottom: 0
  #footer img
    width: 100%
    display: block
</style>
