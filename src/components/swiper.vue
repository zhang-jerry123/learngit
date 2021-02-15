<template>
  <div :class="['swiper',{ column:dir.indexOf('column') > -1 }]">
    <transition :name="trans">
        <div class='swiper_item' :key='act'>
            <slot>
                <img :class='mode' :src="content[act]"/>
            </slot>
        </div>
    </transition>
  </div>
</template>

<script>
export default {
    name:'swiper',
    props:{
        active:{
            type:Number,
            default:0
        },
        content:{
            type:Array,
            default:[]
        },
        duration:{
            type:Number,
            default:5
        },
        mode:{
            type:String,
            default:'aspectfit'
        },
        transition:{
            type:[String,Array],
            default:''
        },
        direction:{
            type:String,
            default:'row',
        },
    },
    data() {
      return {
        act:this.active,
        dir:this.direction,
        trans:''
      }
    },
    methods:{
        setActive(){
            let len = this.content.length
            if (this.dir.indexOf('reverse')>-1){
                this.act = this.act === 0 ? len-1 : --this.act
            }else{
            this.act = this.act === len-1 ? 0 : ++this.act
            }
            this.$emit('onSwiperChange',this.act)
        },
        onSlide () {
           window.clearInterval(this.interval)
           this.interval = window.setInterval(() => {
           this.setActive()
           },this.duration*1000)
        },
        setTransition(){
            let map={
                'row':'slide_left',
                'row-reverse':'slide_right',
                'column':'slide_up',
                'column-reverse':'slide_down'
            }
            this.trans=map[this.dir]
        }

    },
    created(){
            this.setTransition()
            this.onSlide()
            
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
    .swiper{
        display: flex;
        overflow: hidden;
        position: relative;
        height: 100%;
        width: 100%;

        &.column{
            flex-direction: column;
        }

        &_item{
            flex-shrink: 0;
            width: 100%;
            height: 100%;
        }
    }

    img{
        &.aspectfit{
            max-height: 100%;
            max-width: 100%;
        }
        
    }
    .slide{
        &_left{
            &-enter{
                transform: translateX(0);
            }
            &-enter-active{
                transition: all 1s;
            }
            &-enter-to{
                transform: translateX(-100%);
            }
            &-leave{
                transform: translateX(-100%);
            }
            &-leave-active{
                transition: all 1s;
            }
            &-leave-to{
                transform:translateX(-200%);
            }

        }

        &_down{
            &-enter{
                transform:translateY(-200%);
            }
            &-enter-active{
                transition:all 1s;
            }
            &-enter-to{
                transform: translateY(-100%);
            }
            &-leave{
                transform: translateY(0);
            }
            &-leave-active{
                transition: all 1s;
            }
            &-leave-to{
                transform: translateY(100%);
            }
        }
    }

</style>
