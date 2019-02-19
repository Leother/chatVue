<template>
    <div class="getUserType"></div>
</template>

<script>
import { _getCookies } from '@/utils/_getCookies'
import axios from 'axios'
export default {
  name: 'getusertype.vue',
  data () {
    return {}
  },
  methods: {
    _getUserType () {
      let user = _getCookies()
      if (user) {
        axios.get('/api/info', {
          user
        }).then((res) => {
          let data = res.data
          if (data.status === 0) {
            this.$emit('setStateId', data.result._id)
            this.$emit('setStateUserType', data.result.type)
            this.$emit('setStateNike', data.result.nikename)
          }
        })
      }
    }
  },
  mounted () {}
}
</script>

<style scoped>

</style>
