<template>
  <div class="login_container">
    <div class="login_box">
      <!-- 头像区域 -->
      <div class="avatar_box">
        <img src="../assets/loginImg.jpg" />
      </div>
      <!-- 登录表单区域 -->
      <el-form
        ref="ruleFormRef"
        :model="loginFrom"
        class="login_from"
        :rules="loginFromRules"
      >
        <el-form-item prop="username">
          <el-input
            v-model="loginFrom.username"
            prefix-icon="el-icon-user-solid"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            v-model="loginFrom.password"
            prefix-icon="el-icon-unlock"
            show-password
          ></el-input>
        </el-form-item>
        <div class="login_link">
          <el-link
            href="https://element.eleme.io"
            target="_blank"
            type="primary"
            alt="https://element.eleme.io"
            >注册账号</el-link
          >
        </div>
        <el-form-item class="buts">
          <el-button type="success" @click="loginBtn">登录</el-button>
          <el-button type="info" @click="resetForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginFrom: {
        username: 'admin',
        password: '123456',
      },
      loginFromRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 4, max: 8, message: '长度在 4 到 8 个字符', trigger: 'blur' },
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          {
            min: 6,
            max: 15,
            message: '长度在 6 到 15 个字符',
            trigger: 'blur',
          },
        ],
      },
    }
  },
  methods: {
    resetForm() {
      this.$refs.ruleFormRef.resetFields()
    },
    loginBtn() {
      this.$refs.ruleFormRef.validate(async (valid) => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.loginFrom)
        if (res.meta.status !== 200) return this.$Message.error('登录失败！')
        this.$Message.success('登录成功！')
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      })
    },
  },
}
</script>

<style lang="less" scoped>
.login_container {
  background-color: rgb(133, 206, 97);
  height: 100%;
}

.login_box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 8px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);

  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }
  }

  .login_link {
    position: absolute;
    left: 30px;
    bottom: 25px;
  }

  .login_from {
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
  }

  .buts {
    display: flex;
    justify-content: end;
  }
}
</style>