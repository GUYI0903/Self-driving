<template>
  <div class="login-container">
    <div class="login-box">
      <h2>登录</h2>
      <div class="input-group">
        <div class="input-item">
          <i class="fas fa-user"></i>
          <input type="text" placeholder="请输入用户名" />
        </div>
        <div class="input-item">
          <i class="fas fa-lock"></i>
          <input type="password" placeholder="请输入用户密码" />
        </div>
      </div>
      <div class="login-options">
        <label class="remember-pwd">
          <input type="checkbox" />
          <span>记住密码</span>
        </label>
        <a href="#" class="forgot-pwd" @click.prevent="forgotPassword">忘记密码？</a>
      </div>
      <button class="login-btn">登录</button>
      <div class="register-link">
        还没有账号？<a href="#" @click.prevent="goToRegister">立即注册</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginView',
  methods: {
    goToRegister() {
      this.$router.push('/register')
    },
    forgotPassword() {
      // 处理忘记密码的逻辑
      alert('忘记密码功能开发中...')
    }
  }
}
</script>

<style scoped>
.login-container {
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('@/assets/login-bg.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

.login-box {
  width: 400px;
  padding: 40px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 10px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.login-box h2 {
  text-align: center;
  margin-bottom: 30px;
  color: #333;
  font-size: 24px;
}

.input-group {
  margin-bottom: 20px;
}

.input-item {
  position: relative;
  margin-bottom: 20px;
}

.input-item i {
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  color: #999;
}

.input-item input {
  width: 100%;
  padding: 12px 20px 12px 45px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  outline: none;
  transition: all 0.3s;
}

.input-item input:focus {
  border-color: #2196F3;
  box-shadow: 0 0 0 2px rgba(33, 150, 243, 0.1);
}

.login-options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.remember-pwd {
  display: flex;
  align-items: center;
  cursor: pointer;
  user-select: none;
}

.remember-pwd input[type="checkbox"] {
  margin-right: 8px;
}

.remember-pwd span {
  color: #666;
  font-size: 14px;
}

.forgot-pwd {
  color: #2196F3;
  font-size: 14px;
  text-decoration: none;
}

.forgot-pwd:hover {
  text-decoration: underline;
}

.login-btn {
  width: 100%;
  padding: 12px;
  background: #2196F3;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-bottom: 15px;
}

.login-btn:hover {
  background: #1976D2;
}

.register-link {
  text-align: center;
  font-size: 14px;
  color: #666;
}

.register-link a {
  color: #2196F3;
  text-decoration: none;
  margin-left: 5px;
}

.register-link a:hover {
  text-decoration: underline;
}
</style> 