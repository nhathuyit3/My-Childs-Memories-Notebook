<template>
  <div class="book-page toc-page">
    <div class="page-content">
      <div class="toc-header">
        <span class="toc-badge">TABLE OF CONTENTS</span>
        <h2 class="toc-title">Mục Lục Hành Trình</h2>
        <div class="toc-divider">❖ ❖ ❖</div>
      </div>

      <!-- Danh sách các Giai Đoạn trong Mục lục -->
      <div class="toc-list">
        <div 
          v-for="(stage, index) in milestones" 
          :key="stage.id" 
          class="toc-item"
          @click="$emit('go-to-page', index + 2)"
        >
          <div class="toc-item-left">
            <span class="toc-num">0{{ index + 1 }}</span>
            <div class="toc-text">
              <h4 class="toc-stage-title">{{ stage.stageTitle }}</h4>
              <span class="toc-time">{{ stage.timeRange }}</span>
            </div>
          </div>
          <div class="toc-dots"></div>
          <span class="toc-page-num">Trang 0{{ index + 2 }}</span>
        </div>
      </div>

      <div class="toc-footer">
        <p class="toc-note">Chạm vào mỗi giai đoạn để xem ký ức chi tiết</p>
        <span class="page-number">- Trang 1 -</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookTOCPage',
  props: {
    milestones: Array
  },
  emits: ['go-to-page']
}
</script>

<style scoped>
.toc-page {
  background: #fdfbf7;
  padding: 20px;
  height: 100%;
  box-sizing: border-box;
}

.page-content {
  border: 1px solid #ebdcd0;
  height: 100%;
  padding: 24px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.toc-header {
  text-align: center;
}

.toc-badge {
  font-family: 'Cinzel', serif;
  font-size: 0.65rem;
  letter-spacing: 2.5px;
  color: #b08d57;
  font-weight: 700;
}

.toc-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 2.2rem;
  color: #4a3a31;
  margin: 6px 0 4px 0;
  font-weight: 600;
}

.toc-divider {
  color: #c09c5d;
  font-size: 0.75rem;
  letter-spacing: 4px;
}

.toc-list {
  margin: 20px 0;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.toc-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  padding: 8px 10px;
  border-radius: 6px;
  transition: background 0.2s ease;
}

.toc-item:hover {
  background: #f5ece0;
}

.toc-item-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.toc-num {
  font-family: 'Cinzel', serif;
  font-size: 1.1rem;
  color: #b08d57;
  font-weight: 700;
}

.toc-stage-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.15rem;
  color: #4a3a31;
  margin: 0;
  font-weight: 600;
}

.toc-time {
  font-size: 0.72rem;
  color: #8c786c;
}

.toc-dots {
  flex-grow: 1;
  margin: 0 12px;
  border-bottom: 1.5px dotted #d1c0aa;
  height: 12px;
}

.toc-page-num {
  font-family: 'Cinzel', serif;
  font-size: 0.78rem;
  color: #70584c;
  font-weight: 600;
}

.toc-footer {
  text-align: center;
}

.toc-note {
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  font-size: 0.85rem;
  color: #a08c7d;
  margin: 0 0 8px 0;
}

.page-number {
  font-family: 'Cinzel', serif;
  font-size: 0.68rem;
  color: #a89485;
}
</style>