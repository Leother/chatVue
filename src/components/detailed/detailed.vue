<template>
    <div class="detailed">
      <mu-container class="deta-list">
        <mu-tabs :value.sync="active3" class="tabs" center color="#00daca">
          <mu-tab>
            我是求职者
          </mu-tab>
          <mu-tab>
            我是企业
          </mu-tab>
        </mu-tabs>
        <div class="demo-text" v-if="active3 === 0">
          <mu-form :model="value">
            <mu-form-item label="请输入昵称" prop="username">
              <mu-text-field v-model="value.nikename" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入年龄" prop="username">
              <mu-text-field v-model="value.age" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入求职岗位" prop="username">
              <mu-text-field v-model="value.title" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请选择学历" prop="username">
              <mu-select :change="onSeleducChange(normal.value1)"  v-model="normal.value1" full-width>
                <mu-option v-for="(option,index) in options" :key="index" :label="option.title" :value="option.title" ></mu-option>
              </mu-select>
            </mu-form-item>
            <mu-form-item label="请输入工龄" prop="username">
              <mu-text-field v-model="value.years" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入期望工资" prop="username">
              <mu-select :change="onSelmoneyChange(normal.money_value)"  v-model="normal.money_value" full-width>
                <mu-option v-for="(money,index) in moneys" :key="index" :label="money.title" :value="money.title" ></mu-option>
              </mu-select>
            </mu-form-item>
            <mu-form-item label="请输入所在地址" prop="username">
              <mu-text-field v-model="value.address" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入到岗时间" prop="username">
            <mu-text-field v-model="value.arrivaltime" prop="username"></mu-text-field>
          </mu-form-item>
            <mu-form-item label="请输入联系电话" prop="username">
              <mu-text-field v-model="value.del" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入个人简介">
              <textarea v-model="value.doc" class="doc"></textarea>
            </mu-form-item>
          </mu-form>
        </div>
        <div class="demo-text" v-if="active3 === 1">
          <mu-form :model="value">
            <mu-form-item label="请输入企业名称" prop="username">
              <mu-text-field v-model="value.nikename" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入企业规模" prop="username">
              <mu-text-field v-model="value.age" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入招聘岗位" prop="username">
              <mu-text-field v-model="value.title" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请选择学历" prop="username">
              <mu-select :change="onSeleducChange(normal.value1)"  v-model="normal.value1" full-width>
                <mu-option v-for="(option,index) in options" :key="index" :label="option.title" :value="option.title" ></mu-option>
              </mu-select>
            </mu-form-item>
            <mu-form-item label="请输入要求职位工龄" prop="username">
              <mu-text-field v-model="value.years" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入期望工资" prop="username">
              <mu-select :change="onSelmoneyChange(normal.money_value)"  v-model="normal.money_value" full-width>
                <mu-option v-for="(money,index) in moneys" :key="index" :label="money.title" :value="money.title" ></mu-option>
              </mu-select>
            </mu-form-item>
            <mu-form-item label="请输入企业地址" prop="username">
              <mu-text-field v-model="value.address" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入要求到岗时间" prop="username">
              <mu-text-field v-model="value.arrivaltime" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入企业联系电话" prop="username">
              <mu-text-field v-model="value.del" prop="username"></mu-text-field>
            </mu-form-item>
            <mu-form-item label="请输入公司简介">
              <textarea v-model="value.doc" class="doc"></textarea>
            </mu-form-item>
          </mu-form>
        </div>
        <div class="sub-warpeer">
          <mu-button @click="onSubmit" class="sublimt" color="success"> 提 交 </mu-button>
        </div>
      </mu-container>
    </div>
</template>

<script>
import {traversing, indexOfeduc, indexOfmoney, years, del} from '@/utils/traversing'
import axios from 'axios'
export default {
  name: 'detailed',
  data () {
    return {
      active3: 0,
      value: {
        type: 'job',
        nikename: '',
        age: '',
        title: '',
        education: '',
        education_index: '',
        years: '',
        years_index: '',
        money: '',
        money_index: '',
        address: '',
        arrivaltime: '',
        del: '',
        desc: ''
      },
      options: [
        {
          'title': '高中及以下',
          'index': 0
        },
        {
          'title': '大专',
          'index': 1
        },
        {
          'title': '本科',
          'index': 2
        },
        {
          'title': '硕士',
          'index': 3
        },
        {
          'title': '博士',
          'index': 4
        }
      ],
      moneys: [
        {
          'title': '8000及以下'
        },
        {
          'title': '8000-10000'
        },
        {
          'title': '10000-15000'
        },
        {
          'title': '15000-20000'
        },
        {
          'title': '20000-30000'
        },
        {
          'title': '30000以上'
        }
      ],
      normal: {
        value1: '',
        money_value: ''
      }
    }
  },
  methods: {
    onSeleducChange (value) {
      let index = indexOfeduc(value)
      if (index >= 0) {
        this.value.education_index = index
        this.value.education = value
      }
    },
    onSelmoneyChange (value) {
      let index = indexOfmoney(value)
      if (index >= 0) {
        this.value.money_index = index
        this.value.money = value
      }
    },
    getCookies () {
    },
    onSubmit () {
      this.value.years_index = years(this.value.years)
      this.value.type = this.active3 === 0 ? 'job' : 'firm'
      if (!traversing(this.value)) {
        console.log(traversing(this.value))
        return this.$toast.error('所有资料为必填')
      }
      let dels = del(this.value.del)
      if (!dels) return this.$toast.error('请输入正确手机号码')
      axios.post('/api/detailed', {
        user: this.$route.query.user,
        value: this.value
      }).then((res) => {
        let data = res.data
        if (data.status === 0) {
          this.$router.push()
        }
      })
    }
  },
  mounted () {
    this.getCookies()
  }
}
</script>

<style scoped>
.demo-text {
  margin-top: 5rem;
}
  .tabs {
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
  }
.doc {
  outline: none;
  width: 100%;
  height: 6rem;
}
  .sub-warpeer {
    text-align: center;
    margin-bottom: 2rem;
  }
</style>
