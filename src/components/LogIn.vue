<template>
  <Form ref="loginForm" :model="formbean" :rules="rules" @keydown.enter.native="handleSubmit">
    <FormItem prop="userName">
      <Input v-model="formbean.userName" placeholder="请输入用户名">
        <span slot="prepend">
          <Icon :size="16" type="ios-person"></Icon>
        </span>
      </Input>
    </FormItem>
    <FormItem prop="password">
      <Input type="password" v-model="formbean.password" placeholder="请输入密码">
        <span slot="prepend">
          <Icon :size="14" type="md-lock"></Icon>
        </span>
      </Input>
    </FormItem>
    <FormItem label="记住密码">
      <i-switch v-model="formbean.remember" size="large">
        <span slot="open">开</span>
        <span slot="close">关</span>
      </i-switch>
    </FormItem>
    <FormItem>
      <Button @click="handleSubmit" type="primary" long>登录</Button>
    </FormItem>
  </Form>
</template>

<script>
  export default {
    name: 'LogIn',
    props: {
      userNameRules: {
        type: Array,
        default: () => {
          return [{ required: true, message: '账号不能为空', trigger: 'blur' }]
        }
      },
      passwordRules: {
        type: Array,
        default: () => {
          return [{ required: true, message: '密码不能为空', trigger: 'blur' }]
        }
      },
      userpwd: {
        type: String,
        default: ''
      },
      username: {
        type: String,
        default: ''
      }
    },
    data () {
      return {
        formbean: {
          userName: this.username,
          password: this.userpwd,
          remember: false
        }
      }
    },
    computed: {
      rules () {
        return {
          userName: this.userNameRules,
          password: this.passwordRules
        }
      }
    },
    methods: {
      handleSubmit () {
        this.$refs.loginForm.validate(valid => {
          if (valid) {
            this.$emit('on-success-valid', {
              userName: this.formbean.userName,
              password: this.formbean.password,
              remember: this.formbean.remember
            })
          }
        })
      }
    }
  }
</script>

<style scoped>

</style>
