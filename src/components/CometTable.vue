<template>
  <div class="hello">
    <h1>Comet</h1>

    <table>
      <thead>
        <tr>
          <th v-for="key in keys">{{ keyMap[key] || key }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="expirement in expirements" class="expirement">
          <td v-for="key in keys">{{ expirement[key] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import _ from 'lodash'

const keyMap = {
  apiKey: 'Api Key',
  runId: 'Run ID'
}

const keyIndeces = {
  runActive: 4,
  apiKey: 2
}

export default {
  name: 'cometTable',
  props: {
    expirements: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      keyMap
    }
  },
  computed: {
    keys () {
      let allKeys = _.flatMap(this.expirements, expirement => {
        return Object.keys(expirement)
      })

      // better solution idea (ran out of time):
      // [undefined, 'apiKey', undefined]

      _.each(keyIndeces, (value, key) => {
        let currentIndex = allKeys.indexOf(key)
        allKeys.splice(currentIndex, 1)
        allKeys.splice(value, 0, key)
      })

      return _.uniq(allKeys)
    }
  }
}
</script>

<style lang="sass" scoped>

</style>
