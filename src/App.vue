<template>
  <div id="app">
    <slide :slides="slides" :inv="inv" :style="styleObject" :name="transitionName1" :target="target"></slide>
    <slide :slides="slides" :inv="inv" :style="styleObject" :name="transitionName2" :target="target"></slide>
  </div>
</template>

<script>
import slide from './components/Slide.vue'
export default {
  name: 'app',
  components: {
    slide
  },
  data(){
    return {
      slides: [
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913974588712_tsRvc.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14915894814419_zNYsr.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913784864515_mkpqH.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14908694250786_fObqa.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913755624659_gRtNH.jpg',
            href: ''
          }
        ],
        inv: 3000,
        styleObject: {
          width: '1226px',
          height: '460px'
        },
        transitionName1: 'move',
        transitionName2: 'fade',
        target: '_blank',
        timmer: null
    }
  },
  created(){
  },
  computed: {
  },
  methods:{
    show(){
      console.log('shoshoshoshosh')
    }
  }
}
</script>

<style lang="scss">
*{
  margin:0;padding: 0;
  box-sizing: border-box;
}
</style>
