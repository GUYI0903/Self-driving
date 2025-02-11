<script>
export default {
  name: 'ScenicView',
  data() {
    return {
      carouselTexts: [
        {
          title: '故宫博物院',
          desc: '世界上现存规模最大、保存最完整的木质结构古建筑群'
        },
        {
          title: '长城',
          desc: '中国古代伟大的防御工程，世界文化遗产'
        },
        {
          title: '西湖',
          desc: '中国十大风景名胜之一，人间天堂'
        },
        {
          title: '黄山',
          desc: '奇松、怪石、云海、温泉、冬雪五绝闻名于世'
        }
      ],
      scenicSpots: [
        {
          name: '泰山',
          image: '/images/taishan.jpg',
          description: '泰山是中国五岳之首，位于山东省中部。以气势磅礴、雄伟高大而著称，有"天下第一山"之称。这里不仅有壮丽的自然风光，还有深厚的文化底蕴，是自然与人文的完美结合。'
        },
        {
          name: '趵突泉',
          image: '/images/baotoquan.jpg',
          description: '趵突泉位于济南市区，是泉城济南的象征，有"天下第一泉"之称。泉水四季喷涌，昼夜不息，水质清冽甘甜，是济南最负盛名的景点之一。'
        },
        {
          name: '崂山',
          image: '/images/laoshan.jpg',
          description: '崂山位于青岛市东部，是中国海岸线上最高的山，也是道教名山。这里山海相连，风景秀丽，有"海上名山第一"的美誉，是登山观海的绝佳去处。'
        },
        {
          name: '蓬莱阁',
          image: '/images/penglai.jpg',
          description: '蓬莱阁位于烟台蓬莱市，是中国四大名阁之一。这里不仅有气势恢宏的古建筑群，还有神奇的海市蜃楼景观，是一个充满传奇色彩的旅游胜地。'
        }
      ]
    }
  }
}
</script>

<template>
  <div class="page-container">
    <!-- 顶部导航 -->
    <div class="nav-section">
      <div class="nav-buttons">
        <button class="nav-btn" @click="$router.push('/')">
          <span>首页</span>
        </button>
        <button class="nav-btn" @click="$router.push('/route')">
          <span>路线规划</span>
        </button>
        <button class="nav-btn" @click="$router.push('/destination')">
          <span>目的地推荐</span>
        </button>
        <button class="nav-btn active">
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

      <!-- 景点推荐部分 -->
      <div class="content-wrapper">
        <div class="scenic-section">
          <div class="scenic-card" v-for="scenic in scenicSpots" :key="scenic.name">
            <div class="scenic-image">
              <img :src="scenic.image" :alt="scenic.name">
            </div>
            <div class="scenic-info">
              <h3>{{ scenic.name }}</h3>
              <p>{{ scenic.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* 添加导航栏样式 */
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
  width: 100%;
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

@media (max-width: 768px) {
  .placeholder-text h2 {
    font-size: 36px;
  }

  .placeholder-text p {
    font-size: 18px;
  }
}

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.scenic-section {
  padding: 40px 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(800px, 1fr));
  gap: 20px;
}

.scenic-card {
  display: flex;
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  height: 200px;
}

.scenic-image {
  width: 250px;
  overflow: hidden;
}

.scenic-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.scenic-info {
  flex: 1;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.scenic-info h3 {
  font-size: 24px;
  margin-bottom: 12px;
  color: #333;
}

.scenic-info p {
  font-size: 14px;
  line-height: 1.6;
  color: #666;
}

@media (max-width: 1200px) {
  .scenic-section {
    grid-template-columns: 1fr;
    padding: 20px;
  }
}

@media (max-width: 768px) {
  .scenic-card {
    flex-direction: column;
    height: auto;
  }

  .scenic-image {
    width: 100%;
    height: 180px;
  }

  .scenic-info {
    padding: 15px;
  }

  .content-wrapper {
    padding: 0 15px;
  }
}
</style> 