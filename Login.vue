<template>
  <div class="login">
    <Row>
      <Col span="16" style="transform: translate(-3%, 3%); ">
        <LoginSvg class="hero-warp" ref="loginSvg" />
      </Col>
      <Col span="8">
        <Form ref="login" :model="login" :rules="ruleValidate" class="login-warp no-shadow">
          <div class="title tl">
            <i-svg class="page-svg" style="width:296px; width: 282px; transform: scale(1.55); margin-left: 111px;margin-top:15px;margin-bottom:7px;"svgName="AppLogoLogin"></i-svg>
            <p class="login-time"  style="positon:inherit;margin-left:369px;margin-top:11px;">3月15 木 9：29</p>
          </div>
          <div class="login-content">
            <p class="login-label">{{ $t('login.account') }}</p>
            <FormItem class="login-item" prop="username">
              <Input
                prefix="ios-contact"
                v-model="login.username"
                @keyup.enter.native="loging"
                :placeholder="$t('login.account')"
              />
            </FormItem>
            <p class="login-label">{{ $t('login.password') }}</p>
            <FormItem class="login-item" prop="password">
              <Input
                prefix="md-key"
                v-model="login.password"
                @keyup.enter.native="loging"
                :placeholder="$t('login.password')"
                type="password"
                autocomplete="new-password"
              />
            </FormItem>
            <Row :gutter="16" class="mt10 mb5">
              <Col span="12"><Button type="primary" size="large" ghost long>出勤</Button></Col>
              <Col span="12"><Button size="large" long>退勤</Button></Col>
            </Row>
            <FormItem class="login-btn">
              <Button @click="loging" type="primary" size="large" :loading="loading" long>
                {{ $t('login.login') }}
              </Button>
            </FormItem>
          </div>
        </Form>
      </Col>
    </Row>
  </div>
</template>

<script>
import LoginSvg from '@/assets/AnimatedSvg/LoginSvg'
import Logo from '@/assets/AnimatedSvg/Logo'
import { mapActions } from 'vuex'
export default {
  name: 'login',
  components: {
    LoginSvg,
    Logo
  },
  metaInfo: {
    title: 'office-next',
    meta: [
      {
        // set meta
        name: 'keyWords',
        content: 'school web work management'
      },
      {
        name: 'author',
        content: 'Nisshin Scientia'
      }
    ]
    // link: [
    //   {
    //     rel: 'asstes',
    //     href: 'https://assets-cdn.github.com/'
    //   }
    // ]
  },
  data: function() {
    return {
      userCode: '',
      password: '',
      login: {
        username: '',
        password: ''
      },
      loading: false,
      ruleValidate: {
        username: [
          {
            required: true,
            message: this.$t('login.warn.account'),
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: this.$t('login.warn.password'),
            trigger: 'blur'
          }
        ]
      }
    }
  },
  computed: {},
  methods: {
    ...mapActions(['Action_Login']),
    loging() {
      this.$refs.login.validate(valid => {
        if (valid) {
          const value = {
            username: this.login.username,
            password: this.login.password,
            lang: localStorage.getItem('locale') || 'ja_jp'
          }
          this.utils.setStorage('UI_menuType', { type: value.username })
          this.Action_Login({ value, context: this })
        }
      })
    }
  }
}
</script>
<style lang="scss" scoped>
.login {
  max-width: 1920px;
  min-width: 1280px;
  height: 100vh;
  margin: 0 auto;
  background: rgb(247, 247, 247);
  .hero-warp {
    height: 90vh;
    @media (max-width: 1280px) {
      position: relative;
      width: 900px;
    }
  }
  .login-warp {
    width: 520px;
    transform: translateY(18%) scale(0.9);
    overflow: hidden;
    background: $white;
    border-radius: 20px;
    box-shadow: 0 0 1px rgba(0, 0, 0, 0.2), 0 2px 4px rgba(0, 0, 0, 0.1);
    @media (min-height: 800px) {
      transform: translateY(22%) scale(0.9);
    }
    .title {
      background: $primary-background;
      padding: 20px;
    }
    .login-content {
      flex-direction: column;
      justify-content: space-around;
      display: flex;
      padding: 20px 26px;
      height: 400px;
      .login-label {
        display: inline-block;
        text-align: left;
        font-size: 16px;
        font-weight: bold;
        color: rgb(128, 134, 149);
      }
    }
  }
  // .login-item {
  // }
  // .login-btn {
  // }
  .login-time {
    position: absolute;
    right: 13px;
    top: 45px;
    font-size: 16px;
    color: $white;
  }
  /deep/ {
    .ivu-input-prefix {
      padding-left: 25px;
      i {
        font-size: 30px;
        line-height: 50px;
      }
    }
    .ivu-input {
      height: 50px;
      padding-left: 73px;
      border-color: $input-border-grey;
    }
  }
}
</style>
