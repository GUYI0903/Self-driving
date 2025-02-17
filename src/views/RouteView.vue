<template>
  <div class="page-container">
    <!-- 顶部导航 -->
    <div class="nav-section">
      <div class="nav-buttons">
        <button class="nav-btn" @click="$router.push('/')">
          <span>首页</span>
        </button>
        <button class="nav-btn active">
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

    <div class="route-container">
      <!-- 左侧路线规划面板 -->
      <div class="route-panel">
        <div class="route-form">
          <div class="location-input">
            <div class="input-item">
              <label>起</label>
              <input type="text" placeholder="请输入起点" v-model="startPoint" />
              <button class="location-btn" @click="useMyLocation">
                <i class="fas fa-map-marker-alt"></i>
                我的位置
              </button>
            </div>
            <div class="input-item" v-for="(point, index) in viaPoints" :key="index">
              <label>经</label>
              <input type="text" placeholder="请输入途经点" :value="point" @input="updateViaPoint(index, $event.target.value)" />
              <button class="remove-btn" @click="removeViaPoint(index)">
                <i class="fas fa-minus"></i>
              </button>
            </div>
            <div class="input-item">
              <label>终</label>
              <input type="text" placeholder="请输入终点" v-model="endPoint" />
              <button class="add-btn" @click="addViaPoint">
                <i class="fas fa-plus"></i>
              </button>
            </div>
          </div>
          <button class="search-btn" @click="searchRoute">开车去</button>
        </div>

        <!-- 历史记录 -->
        <div class="history-records">
          <h3>历史记录</h3>
          <div class="record-list">
            <div v-for="(record, index) in historyRecords" :key="index" class="record-item">
              <div class="record-content">
                <div class="record-points">
                  <span>{{ record.start }}</span>
                  <i class="fas fa-arrow-right"></i>
                  <span>{{ record.end }}</span>
                </div>
                <div class="record-time">{{ record.time }}</div>
              </div>
              <button class="use-record-btn" @click="useHistoryRecord(record)">使用</button>
              <button class="delete-record-btn" @click="deleteHistoryRecord(index)">删除</button>
            </div>
          </div>
        </div>
      </div>

      <!-- 右侧地图容器 -->
      <div class="map-container" id="container">
        <div class="map-controls">
          <button class="zoom-btn" @click="zoomIn">+</button>
          <button class="zoom-btn" @click="zoomOut">-</button>
          <button class="locate-btn" @click="useMyLocation">
            <i class="fas fa-map-marker-alt"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RouteView',
  data() {
    return {
      map: null,
      startPoint: '',
      viaPoints: [], // 用于存储途经点
      endPoint: '',
      historyRecords: [] // 用于存储历史记录
    }
  },
  mounted() {
    // 延迟初始化地图，确保容器已经渲染
    this.$nextTick(() => {
      this.initMap()
    })
  },
  methods: {
    initMap() {
      // 初始化高德地图
      this.map = new AMap.Map('container', {
        zoom: 11,
        center: [116.397428, 39.90923], // 默认中心点
        resizeEnable: true // 启用自动调整大小
      })
    },
    useMyLocation() {
      // 获取当前位置
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
          const { longitude, latitude } = position.coords;
          this.startPoint = '当前位置'; // 设置起点为当前位置
          this.map.setCenter([longitude, latitude]); // 更新地图中心点
          this.map.setZoom(15); // 可选：放大地图以更好地显示当前位置

          // 可选：在当前位置添加标记
          const marker = new AMap.Marker({
            position: [longitude, latitude],
            title: '我的位置'
          });
          marker.setMap(this.map);
        }, (error) => {
          console.error('获取位置失败', error);
          alert('无法获取当前位置，请检查浏览器的地理位置权限设置。');
        });
      } else {
        alert('浏览器不支持地理位置服务。');
      }
    },
    addViaPoint() {
      this.viaPoints.push(''); // 添加一个空的途经点输入框
    },
    removeViaPoint(index) {
      this.viaPoints.splice(index, 1); // 删除指定的途经点输入框
    },
    updateViaPoint(index, value) {
      this.$set(this.viaPoints, index, value); // 更新途经点的值
    },
    searchRoute() {
      // 在这里实现路线规划逻辑
      const waypoints = this.viaPoints.map(point => point.trim()).filter(point => point);
      const route = {
        origin: this.startPoint,
        destination: this.endPoint,
        waypoints: waypoints
      };
      // 调用高德地图的路径规划 API
      AMap.service('AMap.Driving', () => {
        const driving = new AMap.Driving({
          map: this.map,
          panel: 'panel'
        });
        driving.search(route.origin, route.destination, { waypoints: route.waypoints }, (status, result) => {
          if (status === 'complete') {
            console.log('路线规划成功', result);
            // 保存历史记录
            this.historyRecords.push({
              start: this.startPoint,
              end: this.endPoint,
              time: new Date().toLocaleString()
            });
          } else {
            console.error('路线规划失败', result);
          }
        });
      });
    },
    useHistoryRecord(record) {
      this.startPoint = record.start;
      this.endPoint = record.end;
    },
    deleteHistoryRecord(index) {
      this.historyRecords.splice(index, 1); // 删除指定的历史记录
    },
    zoomIn() {
      this.map.setZoom(this.map.getZoom() + 1);
    },
    zoomOut() {
      this.map.setZoom(this.map.getZoom() - 1);
    }
  }
}
</script>

<style scoped>
.page-container {
  width: 100vw;
  height: 100vh;
  background-color: #f5f7fa;
  display: flex;
  flex-direction: column;
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

.route-container {
  margin-top: 60px;
  flex: 1;
  display: flex;
}

.route-panel {
  width: 400px;
  height: 100%;
  background: white;
  padding: 20px;
  box-shadow: 2px 0 10px rgba(0,0,0,0.1);
  overflow-y: auto;
}

.route-form {
  margin-bottom: 30px;
}

.location-input {
  margin-bottom: 20px;
}

.input-item {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
  gap: 10px;
}

.input-item label {
  width: 30px;
  height: 30px;
  background: #2196F3;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
}

.input-item input {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}

.location-btn, .remove-btn, .add-btn {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  display: flex;
  align-items: center;
  gap: 5px;
}

.location-btn {
  background: #e3f2fd;
  color: #2196F3;
}

.remove-btn {
  background: #ffebee;
  color: #f44336;
}

.add-btn {
  background: #e8f5e9;
  color: #4caf50;
}

.search-btn {
  width: 100%;
  padding: 12px;
  background: #2196F3;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}

.history-records {
  margin-top: 30px;
}

.history-records h3 {
  margin-bottom: 15px;
  color: #333;
}

.record-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid #eee;
}

.record-points {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #333;
}

.record-time {
  font-size: 12px;
  color: #999;
  margin-top: 5px;
}

.use-record-btn {
  padding: 6px 12px;
  background: #e3f2fd;
  color: #2196F3;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.delete-record-btn {
  padding: 6px 12px;
  background: #ffebee;
  color: #f44336;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.map-container {
  flex: 1;
  height: 100%;
  position: relative; /* 添加相对定位 */
  z-index: 1; /* 确保地图在上层 */
}

/* 确保地图容器有明确的尺寸 */
#container {
  width: 100%;
  height: 100%;
}

.map-controls {
  position: absolute;
  bottom: 20px; /* 放在右下角 */
  right: 20px;
  display: flex;
  flex-direction: column;
  z-index: 2; /* 确保按钮在地图上方 */
}

.zoom-btn {
  background: #2196F3;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px;
  margin-bottom: 5px;
  cursor: pointer;
}

.locate-btn {
  background: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px;
  cursor: pointer;
}

@media (max-width: 768px) {
  .route-panel {
    width: 100%;
    height: 50%;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    top: auto;
  }

  .map-container {
    height: 50%;
    width: 100%;
  }

  .route-container {
    flex-direction: column;
  }
}
</style>