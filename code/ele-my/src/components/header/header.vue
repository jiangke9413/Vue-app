<template>
  <!--头部-->
  <div class="header">
    <!--头部信息-->
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div class="supports" v-if="seller.supports">
          <span class="icon" :class="supportClasses[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="supports-count" v-if="seller.supports" @click="showMask(true)">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <!--头部公告-->
    <div class="bulletin-wrapper" @click="showMask(true)">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">
        {{seller.bulletin}}
      </span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <!--头部背景-->
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <transition name="fade">
      <!--遮罩-->
      <div class="mask" v-show="maskShow">
        <!--遮罩包裹器-->
        <div class="mask-wrapper clearfix">
          <!--遮罩主体-->
          <div class="mask-main">
            <!--标题-->
            <h1 class="title">{{seller.name}}</h1>
            <!--评星-->
            <div class="star-wrapper">
              <star :score="seller.score" :size="48"></star>
            </div>
            <!--优惠信息-->
            <div class="info">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <!--优惠内容-->
            <ul class="list">
              <li class="item" v-for="support in seller.supports">
                <span class="icon" :class="supportClasses[support.type]"></span>
                <span class="text">{{support.description}}</span>
              </li>
            </ul>
            <!--商家公告-->
            <div class="info">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <!--公告内容-->
            <div class="bulletin">
              <p class="text">
                {{seller.bulletin}}
              </p>
            </div>
          </div>
        </div>
        <!--遮罩页脚-->
        <div class="mask-footer" @click="showMask(false)">
          <span class="icon-close"></span>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>

  import star from '../star/star.vue'

  export default {
    props: ['seller'],
    data () {
      return {
        maskShow: false,
        supportClasses: ["decrease", "discount", "guarantee", "invoice", "special"]
      }
    },
    methods: {
      showMask (isShow) {
        this.maskShow = isShow
      }
    },
    components: {
      star
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/styuls/mixin.styl"
  /*头部*/
  .header
    position relative
    color #fff
    background-color rgba(7,17,27,.5)
    overflow hidden
    /*头部信息*/
    .content-wrapper
      position relative
      padding 24px 12px 18px 24px
      font-size 0
      .avatar
        display inline-block
        vertical-align top
      .content
        display inline-block
        margin-left 16px
        .title
          margin 2px 0  8px 0
          .brand
            display inline-block
            width 30px
            height 18px
            bg-image(brand)
            background-size 30px 18px
            background-repeat no-repeat
            vertical-align top
           /* background-image url(brand@2x.png)
            background-image url(brand@3x.png)*/
          .name
            margin-left 6px
            font-size 16px
            font-weight bold
            line-height 18px
        .description
          font-size 12px
          line-height 12px
          font-weight 200
        .supports
          margin 10px 0 2px 0
          .icon
            display inline-block
            width 12px
            height 12px
            background-size 12px 12px
            background-repeat no-repeat
            vertical-align top
            &.decrease
              bg-image(decrease_1)
            &.discount
              bg-image(discount_1)
            &.guarantee
              bg-image(guarantee_1)
            &.invoice
              bg-image(invoice_1)
            &.special
              bg-image(special_1)
          .text
            margin-left 4px
            font-size 10px
            line-height 12px
            font-weight 200
      .supports-count
        position absolute
        right 12px
        bottom 15px
        height 10px
        line-height 10px
        padding 7px 8px
        border-radius 10px
        background-color rgba(0,0,0,.2)
        .count
          font-size 10px
          line-height 10px
          font-weight 200
        .icon-keyboard_arrow_right
          font-size 10px
          line-height 10px
          font-weight 200
    /*头部公告*/
    .bulletin-wrapper
      position relative
      overflow hidden
      text-overflow ellipsis
      white-space nowrap
      padding 0 22px 0 12px
      background-color rgba(7,17,27,.2)
      .bulletin-title
        display inline-block
        width 22px
        height 12px
        vertical-align top
        margin-top 7px
        background-size 22px 12px
        background-repeat no-repeat
        bg-image(bulletin)
      .bulletin-text
        font-size 10px
        line-height 28px
        font-weight 200
      .icon-keyboard_arrow_right
        position absolute
        right 12px
        bottom 0
        font-size 10px
        line-height 28px
        font-weight 200
    /*头部背景*/
    .background
      position absolute
      left 0
      top 0
      filter:blur(10px)
      z-index -1
      width 100%
      height 100%

    /*遮罩*/
    .mask
      position fixed
      z-index 99
      top 0
      left 0
      width 100%
      height 100%
      background-color rgba(7,17,27,.8)
      overflow auto
      &.fade-enter-active, &.fade-leave-active
        transition: opacity .5s
      &.fade-enter, &.fade-leave-to
        opacity 0
      /*遮罩包裹器*/
      .mask-wrapper
        min-height 100%
        /*遮罩主体*/
        .mask-main
          padding-top 64px
          padding-bottom 64px
          /*标题*/
          .title
            text-align center
            font-size: 16px
          /*评星*/
          .star-wrapper
            margin 16px 0 28px 0

          /*优惠信息  商家公告*/
          .info
            display flex
            width 80%
            margin 0 auto
            .text
              margin 0 12px
            .line
              position relative
              top 8px
              flex 1
              height 1px
              background-color rgba(255,255,255,.2)
          /*优惠内容*/
          .list
            width 80%
            margin 24px auto 28px auto
            .item
              list-style none
              margin-bottom 12px
              &:last-child
                margin-bottom 0
              .icon
                vertical-align top
                display inline-block
                width 16px
                height 16px
                background-size 16px 16px
                background-repeat no-repeat
                &.decrease
                  bg-image(decrease_2)
                &.discount
                  bg-image(discount_2)
                &.guarantee
                  bg-image(guarantee_2)
                &.invoice
                  bg-image(invoice_2)
                &.special
                  bg-image(special_2)
              .text
                font-size 12px
                line-height 12px
                font-weight 200
          /*公告内容*/
          .bulletin
            width 80%
            margin 24px auto 0 auto
            .text
              font-size 12px
              line-height 24px
              font-weight 200
      /*遮罩页脚*/
      .mask-footer
        margin-top -64px
        text-align center
        .icon-close
          font-size 32px
          color rgba(255,255,255,.5)
</style>
