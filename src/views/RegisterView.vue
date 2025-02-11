<template>
  <div class="register-container">
    <div class="register-box">
      <h2>注册</h2>
      <div class="input-group">
        <div class="input-item">
          <i class="fas fa-user"></i>
          <input type="text" placeholder="请输入用户名" />
        </div>
        <div class="input-item">
          <i class="fas fa-envelope"></i>
          <input type="email" placeholder="请输入邮箱" />
        </div>
        <div class="input-item">
          <i class="fas fa-lock"></i>
          <input type="password" placeholder="请输入密码" />
        </div>
        <div class="input-item">
          <i class="fas fa-lock"></i>
          <input type="password" placeholder="请确认密码" />
        </div>
      </div>
      <div class="agreement">
        <label>
          <input type="checkbox" />
          <span>我已阅读并同意服务条款</span>
        </label>
      </div>
      <button class="register-btn">注册</button>
      <div class="login-link">
        已有账号？<a href="#" @click.prevent="goToLogin">立即登录</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RegisterView',
  methods: {
    goToLogin() {
      this.$router.push('/login')
    }
  }
}
</script>

<style scoped>
.register-container {
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

.register-box {
  width: 400px;
  padding: 40px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 10px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.register-box h2 {
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

.agreement {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
}

.agreement label {
  display: flex;
  align-items: center;
  cursor: pointer;
  user-select: none;
}

.agreement input[type="checkbox"] {
  margin-right: 8px;
}

.agreement span {
  color: #666;
  font-size: 14px;
}

.register-btn {
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

.register-btn:hover {
  background: #1976D2;
}

.login-link {
  text-align: center;
  font-size: 14px;
  color: #666;
}

.login-link a {
  color: #2196F3;
  text-decoration: none;
  margin-left: 5px;
}

.login-link a:hover {
  text-decoration: underline;
}
</style> 