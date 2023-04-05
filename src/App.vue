<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld balance="100000" msg="Welcome to Your Vue.js App" rawHtml="<span style='color: red'>이것은 빨간색이어야 합니다.</span>"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  mounted() {
    console.log("컴포넌트가 마운트 됐습니다.")
  },
  components: {
    HelloWorld
  },
  methods:{

  },
  data() {

  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
