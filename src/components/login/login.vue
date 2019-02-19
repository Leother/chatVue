<template>
    <div class="login">
      <div class="title">
        <h1>BOSS直聘</h1>
        <span>互联网招聘神器</span>
      </div>
      <div class="login-wrap">
        <mu-container>
          <mu-text-field placeholder="用户名" color="white" v-model="username" prop="username"></mu-text-field>
          <br />
          <mu-text-field type="password" placeholder="密码" color="white" v-model="password" prop="username"></mu-text-field>
        </mu-container>
        <div class="go-registered"><span>还没有账号, <router-link to="/registered">立即注册</router-link></span></div>
        <mu-button @click="onSubmit" class="btn" color="success"> 登 录 </mu-button>
      </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'login',
  data () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    onSubmit () {
      if (this.username === '' || this.password === '') {
        return
      }
      axios.post('/api/login', {
        user: this.username,
        pwd: this.password
      }).then((res) => {
        let data = res.data
        if (data.status === 0) {
          this.$toast.success(data.result.title)
          setTimeout(() => {
            this.$router.push(`/detailed?user=${data.result.user}`)
          }, 1000)
        } else {
          this.$toast.error(data.result)
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
