<template>
  <section>
    <pixi-renderer
      @tick="update"
      :backgroundColor="0x0078FF"
      :height="480"
      :width="640"
    >
      <pixi-container
        :x="320" :y="240"
        :rotation="-t / 40"
      >
        <pixi-sprite v-for="(sprite, key) in sprites" :key="key"
                     src="/img/logo.png"
                     :x="sprite.x" :y="sprite.y"
                     :scaleX="sprite.scale" :scaleY="sprite.scale"
                     :anchorX="0.5" :anchorY="0.5"
                     :rotation="sprite.angle + t / 60" />
      </pixi-container>
    </pixi-renderer>
  </section>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';


export default {
  name: 'home',
  components: {
    HelloWorld,
  },
  data () {
    return { t: 0, sprites: [] }
  },
  methods: {
    addSprite () {
      this.sprites.push({
        x: 640 * (0.5 - Math.random()),
        y: 480 * (0.5 - Math.random()),
        angle: 2 * Math.PI * Math.random(),
        scale: 0.25 + 0.5 * Math.random(),
      })
    },
    update (dt) { this.t += dt }
  },
  created () {
    this.addSprite()
    this.addSprite()
    this.addSprite()
  }
};
</script>

<style lang="scss" scoped>
  $pc   : 1026px;
  $ipad : 1025px;
  $smp : 670px;
  #cvs_thumnails_box {
    background-color: #f5f5f5;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  #cvs{
    width: 48%;
    height: 100%;
    margin: 1%;
    // @media (max-width: $ipad){
    //   margin-bottom: 0px;
    //   margin-right: 4%;
    //   width: 50%;
    // }
    // @media (max-width: $smp){
    //   margin-bottom: 50px;
    //   width: 100%;
    // }
  }
  #thumbnails{
    width: 48%;
    height: 100%;
    margin: 1%;
    // @media (max-width: $ipad){
    //   width: 45%;
    //   height: 200px;
    // }
    // @media (max-width: $smp){
    //   width: 100%;
    //   height: 130px;
    // }
    display: flex;
    justify-content: left;
    flex-wrap: wrap;
    .thumbnail {
      //border: 1px solid #ddd;
      box-sizing: border-box;
      width: 33%;
      height: 198px;
      @media (max-width: $ipad){
        margin-top:0%;
        width: 120px;
        height: 120px;
      }
      @media (max-width: $smp){
        margin-top:0%;
        width: 23%;
        height: 60px;
      }
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      transition: 0.3s;
      &:hover {
        filter: blur(3px) brightness(0.9)
      }
      @for $i from 0 through 4 {
        &.thumbnail-#{$i} {
          background-image: url('/images/detail/#{$i}.jpg');
        }
      }
    }
  }
</style>
