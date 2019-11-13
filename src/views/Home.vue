<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>process.env example</h1>
    <ul>
      <li v-for="item in content" :key="item">{{item}}</li>
    </ul>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data() {
    return {
      content: ''
    }
  },
  mounted() {
    console.log(process.env.VUE_APP_SECRET, 'mounted')
    this.content = this.normalize(process.env)
  },
  methods: {
    normalize(item) {
      const ret = JSON.stringify(item)
      const leftSign = '{'
      const rightSign = '}'
      const splitSign = ','
      const start = this.reduceBrackets(leftSign, ret)
      const end = this.reduceBrackets(rightSign, start)
      const result = this.reduceComma(splitSign, end)
      return result
    },
    reduceBrackets(flag, str) {
      const red = str.split(flag)
      return red.join()
    },
    reduceComma(flag, str) {
      const spl = str.split(flag)
      const rec = spl.map(item => {
        if(item) {
          return item
        }
      })
      return rec
    }
  }
}
</script>
