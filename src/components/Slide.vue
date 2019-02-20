<template>
  <div class="slide-show" :style="styleObject" @mouseenter="clear" @mouseleave="init">
    <transition-group tag="ul" class="slide-ul" :name="name">
      <li v-for="(item, index) in slides" :key="index" v-show="index === indexNow">
        <a :href="item.href" :target="target">
          <img :src="item.src" alt="">
        </a>
      </li>
    </transition-group>
    <div class="control-wrap">
      <div class="prev" @click="goto(prevIndex)"></div>
      <div class="next" @click="goto(nextIndex)"></div>
    </div>
    <ul class="slide-page">
      <li @click="goto(index)" v-for="(item,index) in slides" :key="index" :class="index === indexNow ? 'active' : ''"></li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'Slide',
  props: {
    slides: {
      type: Array,
      default: [],
    },
    inv: {
      type: Number,
      default: 1000
    },
    name: {
      type: String,
      default: 'move'
    },
    target: {
      type: String,
      default: '_blank'
    },
    styleObject: {
      type: String
    }

  },
  data(){
    return {
      indexNow: 0
    }
  },
  mounted(){
    this.init();
  },
  computed: {
    prevIndex: function(){
      if(this.indexNow === 0){
        return this.slides.length - 1;
      }else{
        return this.indexNow - 1;
      }
    },
    nextIndex(){
      if(this.indexNow === this.slides.length - 1){
        return 0;
      }else{
        return this.indexNow + 1;
      }
    }
  },
  methods:{
    init(){
      this.timmer = setInterval(()=>{
        if(this.indexNow < this.slides.length - 1){
          this.indexNow++;
        }else{
          this.indexNow = 0;
        }
      }, this.inv)
    },
    clear(){
      clearInterval(this.timmer);
    },
    goto(index){
      this.indexNow = index;
    }
  }
}
</script>

<style lang="scss">
*{
  margin:0;padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

.slide-show{
  position: relative;
  overflow: hidden;
  margin-left: 30px;
}

.slide-ul{
  width: 100%;
  height: 100%;
  li {
    position: absolute;
    width: 100%;
    height: 100%;
    img {
      width: 100%;
      height: 100%;
    }
  }
}

.slide-page{
  position: absolute;
  bottom: 20px;
  right: 50px;
  list-style-type: none;
  display: flex;
  li{
    display: inline-block;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #fff;
    margin: 5px;
    border: 1px solid #b80117;
    &.active{
      border: 1px solid #000;
      background: #ccc;
    }
  }
}

.control-wrap{
  div{
    position: absolute;
    width: 41px;
    height: 69px;
    top: 50%;
    transform: translateY(-50%);
  }

  .prev{
    background: url("http://c1.mifile.cn/f/i/2014/cn/icon/icon-slides.png") no-repeat -84px 50%;
    left: 0;
    &:hover{
      background-position-x: 0;
    }
  }

  .next{
    background: url("http://c1.mifile.cn/f/i/2014/cn/icon/icon-slides.png") no-repeat -125px 50%;
    right: 0;
    &:hover{
      background-position-x: -42px;
    }
  }
}


.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}

.move-enter-active {
    transition: all 0.5s ease;
    transform: translateX(0)
  }
  .move-leave-active {
    transition: all 0.5s ease;
    transform: translateX(-100%);
  }
  .move-enter {
    transform: translateX(100%);
  }
  .move-leave {
    transform: translateX(0);
  }
</style>
