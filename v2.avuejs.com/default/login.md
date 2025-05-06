Login 登录组件
==========

Tips

2.2.0+

普通用户登录
------

图片验证码登录
-------

手机号登录
-----

改变字段
----

调整边距
----

```html
<div>
  <h2>普通用户登录</h2>
  <avue-login :option="option" @submit="submit">
  </avue-login>
  <hr />
  <h2>图片验证码登录</h2>
  <avue-login :option="option1" @refresh="refresh" :codesrc="codesrc" @submit="submit">
  </avue-login>
  <hr />
  <h2>手机号登录</h2>
  <avue-login :option="option2" @submit="submit" @send="send" v-model="form">
  </avue-login>
  <hr />
  <h2>改变字段</h2>
  <avue-login :option="option4" @submit="submit" @send="send">
  </avue-login>
  <hr />
  <h2>调整边距</h2>
  <avue-login :option="option3" @submit="submit" @send="send">
  </avue-login>
</div>

<script>
export default {
  data() {
    return {
      codesrc: '',
      form: {},
      option: {
        width: 400,
        time: 60,
        codeType: 'phone', //phone为手机验证码/img为图片验证码
        column: {
          username: {
            label: '用户名',
            autocomplete: 'off',
            rules: { required: true, message: '请输入用户名', trigger: 'blur' }
          },
          password: {
            label: '密码',
            autocomplete: 'off',
            rules: { required: true, message: '请输入密码', trigger: 'blur' }
          },
          code: {
            hide: true
          }
        }
      },
      option1: {
        width: 400,
        codeType: 'img',
        column: {
          username: {
            label: '用户名',
            placeholder: '手机号/邮箱/用户名',
            autocomplete: 'off',
            rules: { required: true, message: '请输入用户名', trigger: 'blur' }
          },
          password: {
            label: '密码',
            autocomplete: 'off',
            rules: { required: true, message: '请输入密码', trigger: 'blur' }
          },
          code: {
            label: '验证码',
            tip: '点击图片可以刷新验证码',
            autocomplete: 'off',
            rules: { required: true, message: '请输验证码', trigger: 'blur' }
          }
        }
      },
      option2: {
        width: 400,
        time: 60,
        codeType: 'phone',
        column: {
          username: {
            label: '手机号',
            prefixIcon: 'el-icon-mobile-phone',
            placeholder: '手机号/邮箱/用户名',
            autocomplete: 'off',
            rules: { required: true, message: '请输入手机号', trigger: 'blur' }
          },
          password: {
            hide: true,
          },
          code: {
            label: '验证码',
            autocomplete: 'off',
            rules: { required: true, message: '请输验证码', trigger: 'blur' }
          }
        }
      },
      option3: {
        width: 400,
        time: 60,
        labelWidth: 120,
        codeType: 'phone',
        column: {
          username: {
            label: '手机号',
            prefixIcon: 'el-icon-mobile-phone',
            placeholder: '手机号/邮箱/用户名',
            autocomplete: 'off',
            rules: { required: true, message: '请输入手机号', trigger: 'blur' }
          },
          password: {
            hide: true,
          },
          code: {
            label: '验证码',
            autocomplete: 'off',
            rules: { required: true, message: '请输验证码', trigger: 'blur' }
          }
        }
      },
      option4: {
        width: 400,
        column: {
          username: {
            label: '用户名',
            tip: '改变字段为user',
            prop: 'user',
          },
          password: {
            label: '密码',
            tip: '改变字段为pass',
            prop: 'pass',
          },
          code: {
            label: '验证码',
            tip: '改变字段为vaild',
            prop: 'vaild',
          }
        }
      }
    }
  },
  mounted() {
    this.refresh();
  },
  methods: {
    refresh() {
      this.$message.success('图片验证码刷新成功')
      this.codesrc = "https://pigx.pig4cloud.com/code?randomStr=" + new Date().getTime();
    },
    send(done) {
      this.$message.success(this.form.username + '验证码发送成功')
      done();
    },
    submit(form) {
      this.$message.success(JSON.stringify(form))
      console.log(form);
    }
  }
}
</script>