<template>
  <div class="destination-page">
    <!-- 顶部导航 -->
    <div class="nav-section">
      <div class="nav-buttons">
        <button class="nav-btn" @click="$router.push('/')">
          <span>首页</span>
        </button>
        <button class="nav-btn" @click="$router.push('/route')">
          <span>路线规划</span>
        </button>
        <button class="nav-btn active">
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

    <div class="main-content">
      <div class="carousel-section">
        <el-carousel :interval="4000" height="400px">
          <el-carousel-item v-for="item in 4" :key="item">
            <div class="carousel-placeholder">
              <div class="placeholder-content">
                <div class="placeholder-text">
                  <h2>{{ carouselTexts[item-1].title }}</h2>
                  <p>{{ carouselTexts[item-1].desc }}</p>
                </div>
              </div>
            </div>
          </el-carousel-item>
        </el-carousel>
      </div>

      <!-- 城市推荐部分 -->
      <div class="content-wrapper">
        <div class="cities-section">
          <div class="city-card" v-for="city in cities" :key="city.name">
            <div class="city-image">
              <img :src="city.image" :alt="city.name">
            </div>
            <div class="city-info">
              <h3>{{ city.name }}</h3>
              <p>{{ city.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DestinationView',
  data() {
    return {
      carouselTexts: [
        {
          title: '度假胜地',
          desc: '享受完美的休闲时光'
        },
        {
          title: '探索自然美景',
          desc: '感受大自然的壮丽与神秘'
        },
        {
          title: '体验文化之旅',
          desc: '探索世界各地独特的人文风情'
        },
        {
          title: '寻觅美食天堂',
          desc: '品味各地特色美食与文化'
        }
      ],
      cities: [
        {
          name: '济南',
          image: '/images/jinan.jpg',
          description: '济南，别称"泉城"，是山东省省会，拥有72处天下名泉，以趵突泉、黑虎泉、珍珠泉为"济南三大名泉"。这里不仅有泉水，还有大明湖、千佛山等著名景点。'
        },
        {
          name: '青岛',
          image: '/images/qingdao.jpg',
          description: '青岛是著名的滨海旅游城市，以红瓦绿树、碧海蓝天闻名。这里有栈桥、八大关、崂山等著名景点，是休闲度假的理想之地。'
        },
        {
          name: '烟台',
          image: '/images/yantai.jpg',
          description: '烟台是一座美丽的滨海城市，拥有优美的海岸线和丰富的自然资源。这里有蓬莱阁、养马岛、长岛等著名景点，是集观光、休闲、度假为一体的旅游胜地。'
        },
        {
          name: '威海',
          image: '/images/weihai.jpg',
          description: '威海是一座风景秀丽的滨海城市，拥有碧海蓝天、金沙滩、绿色山峦等自然景观。这里有刘公岛、威海古城、华夏城等著名景点，是一个适合休闲度假的好去处。'
        }
      ]
    }
  }
};
</script>

<style scoped>
.page-container {
  width: 100%;
  min-height: 100vh;
  background-color: #f5f7fa;
}

.nav-section {
  background: white;
  border-bottom: 1px solid #e0e0e0;
  width: 100%;
  padding: 15px 40px;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

.nav-buttons {
  width: 100%;
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
  padding-top: 80px;
  width: 100%;
}

.carousel-section {
  width: 100%;
  background: #2196F3;
}

:deep(.el-carousel__container) {
  height: 400px !important;
}

:deep(.el-carousel__indicators--outside) {
  margin-top: 20px;
}

:deep(.el-carousel__button) {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.6);
  transition: all 0.3s;
}

:deep(.el-carousel__indicator.is-active .el-carousel__button) {
  background-color: #fff;
  transform: scale(1.2);
}

.carousel-placeholder {
  height: 100%;
  background: transparent;
  position: relative;
}

.placeholder-content {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 40px;
  position: relative;
  z-index: 1;
}

.placeholder-text {
  color: white;
  transform: translateY(-20px);
}

.placeholder-text h2 {
  font-size: 48px;
  margin-bottom: 20px;
  font-weight: 600;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.placeholder-text p {
  font-size: 24px;
  opacity: 0.95;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  max-width: 800px;
  margin: 0 auto;
}

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* 城市推荐部分样式 */
.cities-section {
  padding: 40px 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(800px, 1fr));
  gap: 20px;
}

.city-card {
  display: flex;
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  height: 200px;
}

.city-image {
  width: 250px;
  overflow: hidden;
}

.city-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.city-info {
  flex: 1;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.city-info h3 {
  font-size: 24px;
  margin-bottom: 12px;
  color: #333;
}

.city-info p {
  font-size: 14px;
  line-height: 1.6;
  color: #666;
}

/* 响应式样式调整 */
@media (max-width: 1200px) {
  .main-content {
    padding-top: 70px;
  }

  .cities-section {
    grid-template-columns: 1fr;
    padding: 20px;
  }

  .carousel-section {
    padding: 15px;
  }

  :deep(.el-carousel__item--card) {
    width: 75% !important;
  }
}

@media (max-width: 768px) {
  .main-content {
    padding-top: 60px;
  }

  .city-card {
    flex-direction: column;
    height: auto;
  }

  .city-image {
    width: 100%;
    height: 180px;
  }

  .city-info {
    padding: 15px;
  }

  .content-wrapper {
    padding: 0 15px;
  }
  
  .carousel-section {
    padding: 10px;
  }

  :deep(.el-carousel__item--card) {
    width: 85% !important;
  }

  .placeholder-text h2 {
    font-size: 36px;
  }

  .placeholder-text p {
    font-size: 18px;
  }
}
</style>