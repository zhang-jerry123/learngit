<template>
  <div>
    <h3>轮播一些文字</h3>
    <Swiper class="swiper_text" :content='texts' :duration='5' @onSwiperChange="changeActive">
      <span>{{texts[active]}}</span>
    </Swiper>
    <h3>纵向轮播</h3>
    <Swiper class="swiper_img" :content="images" direction="column-reverse">
    </Swiper>
  </div>
</template>

<script>
import Swiper from './components/swiper.vue'

export default {
  name: 'App',
  components: {
    Swiper
  },
  data(){
    return{
      active:0,
      texts:[
        'vue-y-swiper',
        'From xixibao',
        '炸鸡&啤酒'
      ],
      images:[
        'https://dummyimage.com/360x240/fff3cd/333&text=vue-y-swiper',
        'https://dummyimage.com/360x240/d6d8d9/333&text=vue-y-swiper',
        'https://dummyimage.com/360x240/cce5ff/333&text=vue-y-swiper',
        'https://dummyimage.com/360x240/d4edda/333&text=vue-y-swiper'
      ]
    }
  },
  methods:{
    changeActive(n){
      this.active=n
    }

  }
}
</script>

<style lang="scss" scoped>
.swiper{
  &_text{
    width: 150px;
    text-align: center;
  }
  &_img{
    height: 240px;
  }
}


</style>>

</style>
