<script>
import taishan from '@/assets/carousel/taishan.jpg';
import baotoquan from '@/assets/carousel/baotuquan.jpeg';
import zhanqiao from '@/assets/carousel/zhanqiao.jpeg';
import buluweisi from '@/assets/carousel/buluweisi.jpeg';

export default {
  name: 'ScenicView',
  data() {
    return {
      carouselImages: [
        taishan,
        baotoquan,
        zhanqiao,
        buluweisi
      ],
      scenicSpots: [
        {
          name: '泰山',
          image: taishan,
          description: '泰山是中国五岳之首，位于山东省中部。以气势磅礴、雄伟高大而著称，有"天下第一山"之称。这里不仅有壮丽的自然风光，还有深厚的文化底蕴，是自然与人文的完美结合。'
        },
        {
          name: '趵突泉',
          image: baotoquan,
          description: '趵突泉位于济南市区，是泉城济南的象征，有"天下第一泉"之称。泉水四季喷涌，昼夜不息，水质清冽甘甜，是济南最负盛名的景点之一。'
        },
        {
          name: '栈桥',
          image: zhanqiao,
          description: '栈桥位于青岛市，是青岛的标志性景点之一。这里有美丽的海景和丰富的历史文化，是游客拍照留念的好地方。'
        },
        {
          name: '布鲁维斯号',
          image: buluweisi,
          description: '布鲁维斯号位于威海市，是一处极具特色的网红打卡地。它曾是一艘运输船，如今静静侧卧在海岸边，船身锈迹斑驳却充满故事感。与周边湛蓝的大海、金色的沙滩相互映衬，构建出独特而迷人的景观，是游客们前来打卡拍照、感受别样风情的绝佳选择。'
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
          <el-carousel-item v-for="(image, index) in carouselImages" :key="index">
            <div class="carousel-image">
              <img :src="image" :alt="`carousel-${index + 1}`">
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

.carousel-image {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.carousel-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
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