<template>
  <div
    class="chapter"
    :height="height"
    :style="cssVars"
  >
    <div class="chapterTitle">
      <slot name="chapterTitle">
        Chapter Title
      </slot>
    </div>
    <div
      class="bg"
      :style="cssVars"
    >
      <picture>
        <!--Media size suggestions https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images-->
        <source
          media="(max-width: 799px)"
          :srcset="require(`@/assets/titleImages/1x/${image}-1x.jpg`)"
        >
        <source
          media="(min-width: 800px)"
          :srcset="require(`@/assets/titleImages/2x/${image}-2x.jpg`)"
        >
        <img :src="require(`@/assets/titleImages/2x/${image}-2x.jpg`)">
      </picture>
      <div
        v-if="overlay"
        class="overlay"
      />
    </div>
  </div>
</template>
<script>
export default {
    name: "TestImage",
    props:{
        overlay: {
            type: Boolean,
            default: true
        },
        image: {
            type: String,
            default: `chapter1`
        },
        height:{
            type: Number,
            default: 100
        },
        overlayOpacity:{
            type: Number,
            default: .5
        }
    },
    computed:{
        cssVars(){
            return{
                "--height": `${this.height}vh`,
                "--overlay-opacity": `${this.overlayOpacity}`
            }
        }
    }
}
</script>
<style lang="scss" scoped>
.chapter{
    position: relative;
    height: var(--height);
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}
.overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background: #000;
    opacity: var(--overlay-opacity);
    z-index: 1;
    top:0;
    left: 0;
}
.bg{
    position: absolute;
    top: 0;
    left: 0;
    width:100%;
    height:100%;
    img{
      object-fit: cover;
      object-position: center center;
      width: 100%;
      height: 100%;
    }
    
    // background-image: var(--bg-image);
    // background-position: center;
    // background-size: cover;
    // background-repeat: no-repeat;
}
.chapterTitle{
    position: relative;
    z-index: 2;
    font-size: 2em;
    color: #fff;
    padding: 0 20px;
    text-align: center;
}
</style>