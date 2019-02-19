<template>
    <div class="registered">
      <div class="title">
        <h1>BOSS直聘</h1>
        <span>账号注册</span>
      </div>
      <div class="registered-warpper">
        <mu-container>
          <mu-text-field max-length="16" placeholder="用户名" :help-text="user_error" color="white" v-model="username" prop="username"></mu-text-field>
          <br />
          <mu-text-field max-length="16" type="password" :help-text="pass_error" placeholder="密码" color="white" v-model="password" prop="username"></mu-text-field>
          <br />
          <mu-text-field max-length="16" type="password" :help-text="pass_error" placeholder="重复密码" color="white" v-model="newpass" prop="username"></mu-text-field>
        </mu-container>
      </div>
      <div class="go-login"><span>已经有账号, <router-link to="/login">立即登录</router-link></span></div>
      <mu-button @click="register" class="btn" color="success"> 注 册 </mu-button>
    </div>
</template>

<script>
import {verificantion, verifPass} from '@/utils/verification'
import axios from 'axios'
export default {
  name: 'registered',
  data () {
    return {
      username: '',
      password: '',
      newpass: '',
      user_error: '',
      pass_error: ''
    }
  },
  methods: {
    register () {
      if (this.username === '' || this.password === '' || this.newpass === '') {
        return this.$toast.error('用户名或密码不能为空')
      }
      if (verificantion(this.username)) {
        if (verifPass(this.password, this.newpass)) {
          axios.post('/api/registered', {
            username: this.username,
            password: this.password
          }).then((res) => {
            let data = res.data
            if (data.status === 1) {
              this.$toast.error('用户名已经存在')
            }
            if (data.status === 0) {
              this.$toast.success('注册成功')
              setTimeout(() => {
                this.$router.push('/login')
              }, 1000)
            }
          })
        } else {
          this.$toast.error('密码输入不正确')
          this.pass_error = '密码输入不正确，请输入4-16位数字或字母'
        }
      } else {
        this.$toast.error('用户名输入不正确')
        this.user_error = '用户名输入不正确，请输入4-16位数字或字母'
      }
    }
  }
}
</script>

<style scoped>

</style>
