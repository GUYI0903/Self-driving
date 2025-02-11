<script>
export default {
  name: 'ChatView',
  data() {
    return {
      carouselTexts: [
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
        },
        {
          title: '度假胜地',
          desc: '享受完美的休闲时光'
        }
      ],
      messages: [
        {
          type: 'bot',
          content: `你好！我是你的智能客服，可以为您：
• 推荐旅游目的地
• 规划旅游路线
• 介绍景点信息
• 解答旅游问题
请问有什么可以帮您？`
        }
      ],
      inputMessage: '',
      loading: false,
      apiConfig: {
        apiKey: 'sk-eb96788049e047dfb837511df4b7b2e6'  // 替换为您的 DeepSeek API Key
      }
    }
  },
  methods: {
    async callDeepSeekAPI(message) {
      const url = 'https://api.deepseek.com/v1/chat/completions';
      
      try {
        const response = await fetch(url, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${this.apiConfig.apiKey}`
          },
          body: JSON.stringify({
            model: 'deepseek-chat',
            messages: [
              {
                role: 'system',
                content: '你是一个专业的旅游咨询客服，可以为用户提供旅游目的地推荐、路线规划、景点介绍等服务。请用友善的语气回答用户的问题。专注于山东省的旅游资源。'
              },
              {
                role: 'user',
                content: message
              }
            ],
            temperature: 0.7,
            max_tokens: 2000
          })
        });

        const data = await response.json();
        return data.choices[0].message.content;
      } catch (error) {
        console.error('调用DeepSeek API失败:', error);
        throw error;
      }
    },

    async sendMessage() {
      if (!this.inputMessage.trim() || this.loading) return;

      // 添加用户消息
      this.messages.push({
        type: 'user',
        content: this.inputMessage
      });

      const userMessage = this.inputMessage;
      this.inputMessage = '';
      this.loading = true;

      try {
        // 调用 DeepSeek API
        const response = await this.callDeepSeekAPI(userMessage);
        
        // 添加机器人回复
        this.messages.push({
          type: 'bot',
          content: response
        });
      } catch (error) {
        console.error('Error:', error);
        this.messages.push({
          type: 'bot',
          content: '抱歉，我遇到了一些问题，请稍后再试。'
        });
      }

      this.loading = false;
      
      // 滚动到底部
      this.$nextTick(() => {
        const chatMessages = document.querySelector('.chat-messages');
        chatMessages.scrollTop = chatMessages.scrollHeight;
      });
    },
    scrollToBottom() {
      const chatContainer = this.$refs.chatContainer
      chatContainer.scrollTop = chatContainer.scrollHeight
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
        <button class="nav-btn" @click="$router.push('/scenic')">
          <span>景点推荐</span>
        </button>
        <button class="nav-btn active">
          <span>智能客服</span>
        </button>
      </div>
    </div>

    <div class="main-content">
      <div class="chat-container">
        <!-- 添加聊天头部 -->
        <div class="chat-header">
          <h2>智能客服</h2>
          <p>24小时为您提供专业的旅游咨询服务</p>
        </div>

        <div class="chat-messages">
          <!-- 聊天消息区域 -->
          <div v-for="(message, index) in messages" :key="index" 
               :class="['message', message.type === 'user' ? 'user-message' : 'bot-message']">
            <div class="message-content" v-html="message.content.replace(/\n/g, '<br>').replace(/•/g, '&bull;')"></div>
          </div>
        </div>

        <div class="chat-input">
          <input type="text" 
                 v-model="inputMessage" 
                 placeholder="请输入您的问题..."
                 @keyup.enter="sendMessage">
          <button @click="sendMessage" :disabled="loading">
            {{ loading ? '发送中...' : '发送' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

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
  min-height: calc(100vh - 80px);
  display: flex;
  justify-content: center;
}

.chat-container {
  width: 100%;
  max-width: 1200px;
  height: calc(100vh - 100px);
  margin: 20px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.chat-header {
  padding: 20px;
  background: linear-gradient(135deg, #2196F3, #1976D2);
  color: white;
  border-radius: 12px 12px 0 0;
  text-align: center;
}

.chat-header h2 {
  font-size: 24px;
  margin-bottom: 8px;
  font-weight: 600;
}

.chat-header p {
  font-size: 14px;
  opacity: 0.9;
}

.chat-messages {
  flex: 1;
  padding: 20px;
  overflow-y: auto;
}

.message {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

.user-message {
  align-items: flex-end;
}

.bot-message {
  align-items: flex-start;
}

.message-content {
  max-width: 70%;
  padding: 12px 16px;
  border-radius: 12px;
  font-size: 14px;
  line-height: 1.6;
  white-space: pre-line;
}

.user-message .message-content {
  background: #2196F3;
  color: white;
}

.bot-message .message-content {
  background: #f5f5f5;
  color: #333;
}

.chat-input {
  padding: 20px;
  border-top: 1px solid #eee;
  display: flex;
  gap: 10px;
}

.chat-input input {
  flex: 1;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
  transition: border-color 0.3s;
}

.chat-input input:focus {
  border-color: #2196F3;
}

.chat-input button {
  padding: 12px 24px;
  background: #2196F3;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.chat-input button:hover:not(:disabled) {
  background: #1976D2;
}

.chat-input button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

@media (max-width: 768px) {
  .chat-container {
    margin: 10px;
    height: calc(100vh - 80px);
  }

  .message-content {
    max-width: 85%;
  }

  .chat-input {
    padding: 15px;
  }
}
</style> 