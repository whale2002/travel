<template>
  <div>
    <router-link 
    class="header-abs"
    to="/"
    tag="div"
    v-show="showAbs">
      <i class='iconfont back-icon'>&#xe624;</i>
    </router-link>
    <div 
    class="header-fixed" 
    v-show="!showAbs"
    :style="opacityStyle">
      <router-link to="/">
        <i class='iconfont header-fixed-back'>&#xe624;</i>
      </router-link>
      景点详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data() {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll() {
      const top = document.documentElement.scrollTop
      if(top > 60){
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {
          opacity
        }
        this.showAbs = false
      }
      else this.showAbs = true
    }
  },
  // activated() {
  //   window.addEventListener('scroll',this.handleScroll)
  // },
  // deactivated() {
  //   window.removeEventListener('scroll',this.handleScroll)
  // }
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
  unmounted () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang='less' scoped>
  .header-abs{
    position: absolute;
    left: .2rem;
    top: .2rem;
    width: .8rem;
    height: .8rem;
    line-height: .8rem;
    border-radius: .4rem;
    text-align: center;
    background: rgba(0, 0, 0, .8);
    .back-icon{
      color: #fff;
      font-size: .4rem;
    }
  }
  .header-fixed{
    z-index: 999;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: .86rem;
    line-height: .86rem;
    text-align: center;
    font-size: .32rem;
    color: #fff;
    font-weight: 600;
    background-color: #00bcd4;
    .header-fixed-back{
      width: .64rem;
      text-align: center;
      font-size: .4rem;
      position: absolute;
      top: 0;
      left: 0;
      color: #fff;
    }
   }
</style>