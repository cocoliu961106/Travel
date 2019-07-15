<template>
  <ul class="list">
    <li class="item"
        v-for="item of letters"
        :key="item"
        :ref="item"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        @click="handleLetterClick">
      {{item}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'Alphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    // 城市列表随字母表拖动显示算法
    handleTouchMove (e) {
      if (this.touchStatus) {
        // 运用节流提高运行性能
        if (this.timer) {
          clearTimeout(this.timer)
        }
        // 每个字母距离页面顶部距离
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79
          // 根据手指拖动获取到当前手指所在字母索引
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        })
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  updated () {
    // 第一个字母距离搜索框距离
    this.startY = this.$refs['A'][0].offsetTop
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .list
    display flex
    flex-direction column
    justify-content center
    position absolute
    top 1.58rem
    right 0
    bottom 0
    width .4rem

    .item
      line-height .4rem
      text-align center
      color $bgColor

</style>
