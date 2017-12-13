<template>
  <div id="app">
    <CometTable v-bind:expirements="expirements"/>
  </div>
</template>

<script>
import CometTable from './components/CometTable'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    CometTable
  },
  data () {
    return {
      expirements: []
    }
  },
  mounted () {
    const api = 'https://staging.comet.ml/api/public-logger/get/runs?apiKey=Jon-Snow'
    axios.get(api).then(res => {
      this.expirements = res.data
    })
  }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>
