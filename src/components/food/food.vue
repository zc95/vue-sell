<template>
    <transition name="move">
        <div v-show="showFlag" class="food" ref="food">
            <div class="food-content">
                <div class="image-header">
                     <img :src="food.image">
                     <div class="back" @click="show">
                    <i class="icon-arrow_lift"></i>
                </div>
                </div>
                <div class="content">
                    <h1 class="title">{{food.name}}</h1>
                    <div class="detail">
                        <span class="sell-count">月售{{food.sellCount}}份</span>
                        <span class="rating">好评率{{food.rating}}%</span>
                    </div>
                    <div class="price">
                        <span class="now">￥{{food.price}}</span><span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script type="text/ecmascript-6">
import BScroll from 'better-scroll';
export default {
  props: {
    food: {
      type: Object
    }
  },
  data() {
    return {
      showFlag: false
    };
  },
  methods: {
    show() {
      this.showFlag = !this.showFlag;
      this.$nextTick(()=>{
          if(!this.scroll){
              this,scroll = new BScroll(this.$refs.food,{
                  click: true
              })
          }else{
              this.scroll.refresh();
          }
      })
    }
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
.food {
    position: fixed;
    left: 0;
    top: 0;
    bottom: 48px;
    z-index: 30;
    width: 100%;
    background: #fff;
    transform: translate3d(0, 0, 0);

    &.move-enter-active, &.move-leave-active {
        transition: all 0.2s linear;
    }

    &.move-enter, &.move-leave-active {
        transform: translate3d(100%, 0, 0);
    }

    .image-header {
        position: relative;
        width: 100%;
        height: 0;
        padding-top: 100%;

        img {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .back {
            position: absolute;
            top: 10px;
            left: 0;

            .icon-arrow_lift {
                display: block;
                padding: 10px;
                font-size: 20px;
                color: #fff;
            }
        }
    }

    .content {
        padding: 18px;

        .title {
            line-height: 14px;
            margin-bottom: 8px;
            font-size: 14px;
            font-weight: 700;
            color: rgb(7, 17, 27);
        }

        .detail {
            line-height: 10px;
            height: 10px;
            margin-bottom: 18px;
            font-size: 0;

            .sell-count, .rating {
                font-size: 10px;
                color: rgb(147, 153, 159);
            }

            .sell-count {
                margin-right: 12px;
            }
        }

        .price {
            font-weight: 700;
            line-height: 24px;

            .now {
                margin-right: 8px;
                font-size: 14px;
                color: rgb(240, 20, 20);
            }

            .old {
                text-decoration: line-through;
                font-size: 10px;
                color: rgb(147, 153, 159);
            }
        }
    }
}
</style>


