<template>
  <page class="goods-list-view" :title="$t('examples.goodsList')">
    <div slot="content">
      <scroll ref="scroll">
        <ul class="foods-wrapper">
          <li @click="selectFood(food,$event)" v-for="food in foods" class="food-item border-1px">
            <div class="icon">
              <img width="57" height="57" :src="food.icon">
            </div>
            <div class="content">
              <h2 class="name">{{food.name}}</h2>
              <p class="desc">{{food.description}}</p>
              <div class="extra">
                <span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
              </div>
              <div class="price">
                <span class="now">￥{{food.price}}</span>
                <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
              </div>
            </div>
          </li>
        </ul>
      </scroll>
    </div>
  </page>
</template>

<script>
  import Page from 'example/components/page/page.vue'
  import Scroll from 'example/components/scroll/scroll'
  import data from 'example/data/goods-list.json'

  let _foods = []

  data.goods.forEach((item) => {
    _foods = _foods.concat(item.foods)
  })
  while (_foods.length < 100) {
    _foods = _foods.concat(_foods)
  }

  export default {
    data() {
      return {
        foods: _foods
      }
    },
    components: {
      Page,
      Scroll
    }
  }
</script>

<style lang="stylus">
  @import "~common/stylus/mixin.styl"

  .page
    &.goods-list-view
      .wrapper
        .content
          margin: 0
  .foods-wrapper
    .food-item
      display: flex
      margin: 18px
      padding-bottom: 18px
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      &:last-child
        border-none()
        margin-bottom: 0
      .icon
        flex: 0 0 57px
        margin-right: 10px
      .content
        flex: 1
        .name
          margin: 2px 0 8px 0
          height: 14px
          line-height: 14px
          font-size: 14px
          color: rgb(7, 17, 27)
        .desc, .extra
          line-height: 10px
          font-size: 10px
          color: rgb(147, 153, 159)
        .desc
          line-height: 12px
          margin-bottom: 8px
        .extra
          .count
            margin-right: 12px
        .price
          font-weight: 700
          line-height: 24px
          .now
            margin-right: 8px
            font-size: 14px
            color: rgb(240, 20, 20)
          .old
            text-decoration: line-through
            font-size: 10px
            color: rgb(147, 153, 159)
        .cartcontrol-wrapper
          position: absolute
          right: 0
          bottom: 12px
</style>
