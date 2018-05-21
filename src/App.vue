<template>
  <div id="app">
    <p>通过键盘上下键和按钮控制数值大小</p>
    <number v-model="value" :max="max" :min="min"></number>
  </div>
</template>

<script>
import number from '@/components/number'
export default {
  name: 'App',
  data () {
    return {
      value: 5,
      max: 10,
      min: 0
    }
  },
  computed: {

  },
  components: {
    number
  },
  methods: {
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
