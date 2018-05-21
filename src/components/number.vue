<template>
  <div class="input-number">
    <input type="text" :value="currentValue" @click="handleChange" @keydown="numberFocus"/>
    <button @click="handleDown" :disabled="currentValue <= min">-</button>
    <button @click="handleUp" :disabled="currentValue >= max">+</button>
  </div>
</template>

<script>
// 判断输入的是否为数字
function isValueNumber (value) {
  return (/(^-?[0-9]+\.{1}\d+$)|(^-?[1-9][0-9]*$)|(^-?0{1}$)/).test(value + '')
}
export default {
  name: 'number',
  props: {
    max: {
      type: Number,
      default: Infinity
    },
    min: {
      type: Number,
      default: -Infinity
    },
    value: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      currentValue: this.value
    }
  },
  // 使用watch监听value和currentValue
  watch: {
    currentValue: function (val) {
      this.$emit('input', val)
      this.$emit('on-change', val)
      this.$emit('on-focus', val)
    },
    value: function (val) {
      this.updateValue(val)
    }
  },
  mounted: function () {
    this.updateValue(this.value)
  },
  methods: {
    updateValue (val) {
      if (val > this.max) {
        val = this.max
      }
      if (val < this.min) {
        val = this.min
      }
      this.currentValue = val
    },
    // 通过上下键控制数值
    numberFocus (event) {
      if (event.keyCode === 38) {
        console.log('up')
        if (this.currentValue >= this.max) return
        this.currentValue += 1
      }
      if (event.keyCode === 40) {
        console.log('dwon')
        if (this.currentValue <= this.min) return
        this.currentValue -= 1
      }
    },
    handleChange (event) {
      // 将获得的value值进行去空格操作
      var val = event.target.value.trim()
      var max = this.max
      var min = this.min

      if (isValueNumber(val)) {
        val = Number(val)
        this.currentValue = val

        if (val > max) {
          this.currentValue = max
        } else if (val < min) {
          this.currentValue = min
        }
      } else {
        event.target.value = this.currentValue
      }
    },
    handleDown () {
      if (this.currentValue <= this.min) return
      this.currentValue -= 1
    },
    handleUp () {
      if (this.currentValue >= this.max) return
      this.currentValue += 1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
