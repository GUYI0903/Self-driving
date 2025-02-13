<script>
export default {
  name: 'HomeView',
  data() {
    return {
      carouselImages: [
        '/src/assets/carousel/baotuquan.jpeg',
        '/src/assets/carousel/buluweisi.jpeg',
        '/src/assets/carousel/taishan.jpg',
        '/src/assets/carousel/zhanqiao.jpeg'
      ]
    }
  },
  methods: {
    goToLogin() {
      this.$router.push('/login')
    },
    goToRegister() {
      this.$router.push('/register')
    },
    goToRoute() {
      this.$router.push('/route')
    }
  }
}
</script>

<template>
  <div class="home">
    <!-- 顶部导航栏 -->
    <div class="header">
      <div class="header-content">
        <div class="logo">
          <img src="/src/assets/travel-logo.png" alt="Travel Logo" class="logo-img" />
        </div>
        
        <div class="search-box">
          <div class="search-wrapper">
            <input type="text" placeholder="请输入关键词搜索" />
            <button class="search-btn">搜索</button>
          </div>
        </div>

        <div class="auth-buttons">
          <button class="auth-btn login" @click="goToLogin">登录</button>
          <button class="auth-btn register" @click="goToRegister">注册</button>
        </div>
      </div>
    </div>

    <!-- 导航按钮 -->
    <div class="nav-section">
      <div class="nav-buttons">
        <button class="nav-btn active">
          <span>首页</span>
        </button>
        <button class="nav-btn" @click="goToRoute">
          <span>路线规划</span>
        </button>
        <button class="nav-btn" @click="$router.push('/destination')">
          <span>目的地推荐</span>
        </button>
        <button class="nav-btn" @click="$router.push('/scenic')">
          <span>景点推荐</span>
        </button>
        <button class="nav-btn" @click="$router.push('/chat')">
          <span>智能客服</span>
        </button>
      </div>
    </div>

    <!-- 轮播图 -->
    <div class="main-content">
      <div class="carousel">
        <el-carousel :interval="4000" type="card" height="500px">
          <el-carousel-item v-for="(image, index) in carouselImages" :key="index">
            <div class="carousel-image">
              <img :src="image" :alt="`carousel-${index + 1}`">
            </div>
          </el-carousel-item>
        </el-carousel>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
  background-color: #f5f7fa;
}

.header {
  background-color: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  padding: 20px 0;
  position: fixed;
  width: 100vw;
  top: 0;
  z-index: 100;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}

.header-content {
  width: 100%;
  padding: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

.logo {
  flex: 0 0 auto;
}

.logo-img {
  height: 60px;
  width: auto;
  object-fit: contain;
}

.search-box {
  flex: 0 1 500px;
  margin: 0 auto;
}

.search-wrapper {
  display: flex;
  width: 100%;
  height: 40px;
  border: 1px solid #ddd;
  border-radius: 4px;
  overflow: hidden;
  background: white;
}

.search-box input {
  flex: 1;
  padding: 0 15px;
  border: none;
  outline: none;
  font-size: 14px;
}

.search-btn {
  width: 80px;
  height: 100%;
  border: none;
  background-color: #333;
  color: white;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.search-btn:hover {
  background-color: #000;
}

.auth-buttons {
  flex: 0 0 auto;
  display: flex;
  gap: 15px;
}

.auth-btn {
  padding: 8px 20px;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s;
}

.auth-btn.login {
  background-color: transparent;
  border: 1px solid #2196F3;
  color: #2196F3;
}

.auth-btn.login:hover {
  background-color: #e3f2fd;
}

.auth-btn.register {
  background-color: #2196F3;
  border: 1px solid #2196F3;
  color: white;
}

.auth-btn.register:hover {
  background-color: #1976D2;
}

.nav-section {
  padding-top: 100px;
  background: white;
  border-bottom: 1px solid #e0e0e0;
  width: 100vw;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}

.nav-buttons {
  width: 100%;
  padding: 15px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  border: none;
  background: transparent;
  color: #666;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 14px;
  white-space: nowrap;
}

.nav-btn:hover, .nav-btn.active {
  color: #2196F3;
  background-color: #e3f2fd;
  transform: translateY(-2px);
}

.main-content {
  width: 100vw;
  margin: 30px auto;
  padding: 0 40px;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}

.carousel {
  width: 100%;
  margin-top: 20px;
}

.carousel-image {
  width: 100%;
  height: 100%;
  border-radius: 12px;
  overflow: hidden;
}

.carousel-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

:deep(.el-carousel__item) {
  border-radius: 12px;
}

:deep(.el-carousel__item--card) {
  border-radius: 12px;
}

:deep(.el-carousel__item--card.is-active) {
  transform: scale(1.1);
  transition: all 0.4s ease;
}

@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    gap: 15px;
    padding: 0 20px;
  }

  .search-box {
    width: 100%;
    order: 2;
  }

  .auth-buttons {
    width: 100%;
    order: 3;
    justify-content: center;
  }

  .auth-btn {
    flex: 1;
    max-width: 120px;
  }

  .nav-buttons {
    padding: 15px 20px;
  }

  .nav-btn {
    margin: 0 5px;
  }

  .main-content {
    padding: 0 20px;
  }

  .placeholder-text h2 {
    font-size: 24px;
  }

  .placeholder-text p {
    font-size: 16px;
  }
}
</style>
