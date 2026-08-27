<template>
  <div class="book-page stage-page grid-notebook-bg">
    <div class="page-content">
      <!-- Top Bar dạng viết tay -->
      <div class="stage-top-bar">
        <div class="title-group">
          <span class="stage-number">CHAPTER 0{{ stageIndex + 1 }}</span>
          <h2 class="handwritten-title">{{ stage.stageTitle }}</h2>
        </div>
        <div class="tape-tag">
          <span>🗓️ {{ stage.timeRange }}</span>
        </div>
      </div>

      <!-- Lời nhắn nét chữ viết tay trên ô tập -->
      <p class="handwritten-message" v-if="stage.message">
        "{{ stage.message }}"
      </p>

      <!-- Danh sách ảnh đính Băng keo (Washi Tape) -->
      <div class="album-grid">
        <div 
          v-for="(item, idx) in stage.items" 
          :key="item.id" 
          class="taped-photo-card"
          :style="{ transform: `rotate(${idx % 2 === 0 ? -1.5 : 1.5}deg)` }"
          @click="$emit('open-modal', item)"
        >
          <!-- Miếng băng keo giả lập -->
          <div class="washi-tape top-tape"></div>

          <div class="photo-frame">
            <img :src="item.photoUrl" :alt="item.title" class="photo-img" />
          </div>

          <div class="card-info">
            <h4 class="handwritten-card-title">{{ item.title }}</h4>
            <span class="handwritten-date">{{ item.date }}</span>
          </div>
        </div>
      </div>

      <div class="page-footer">
        <span class="page-number">- Trang {{ stageIndex + 2 }} -</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookStagePage',
  props: { stage: Object, stageIndex: Number },
  emits: ['open-modal']
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&display=swap');

/* Nền giấy kẻ ô tập vàng nhẹ hoài niệm */
.grid-notebook-bg {
  background-color: #f7f2e6;
  background-image: 
    linear-gradient(rgba(218, 203, 182, 0.35) 1px, transparent 1px),
    linear-gradient(90deg, rgba(218, 203, 182, 0.35) 1px, transparent 1px);
  background-size: 18px 18px;
  padding: 20px;
  height: 100%;
  box-sizing: border-box;
}

.page-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.stage-top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px dashed #d1c0aa;
  padding-bottom: 6px;
}

.stage-number { font-family: 'Cinzel', serif; font-size: 0.65rem; color: #b08d57; font-weight: 700; }
.handwritten-title { font-family: 'Caveat', cursive; font-size: 2rem; color: #4a3a31; margin: 0; }

.tape-tag {
  background: rgba(245, 236, 224, 0.8);
  border: 1px solid #d9c5b2;
  padding: 2px 10px;
  font-family: 'Caveat', cursive;
  font-size: 1.1rem;
  color: #6e584c;
}

.handwritten-message {
  font-family: 'Caveat', cursive;
  font-size: 1.45rem;
  color: #57443a;
  margin: 10px 0;
  text-align: center;
  line-height: 1.3;
}

/* Album ảnh dán băng keo */
.album-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin: auto 0;
}

.taped-photo-card {
  position: relative;
  background: #ffffff;
  padding: 8px 8px 12px 8px;
  box-shadow: 0 4px 12px rgba(80, 60, 45, 0.12);
  cursor: pointer;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  /* Đảm bảo thẻ ảnh luôn nổi lên trên cùng để nhận click chuẩn xác */
  z-index: 10; 
  pointer-events: auto;
}

.taped-photo-card:hover {
  transform: scale(1.04) rotate(0deg) !important;
  z-index: 5;
  box-shadow: 0 8px 20px rgba(80, 60, 45, 0.2);
}

/* Miếng băng keo Washi Tape trong suốt */
.washi-tape {
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 55px;
  height: 18px;
  background: rgba(235, 222, 195, 0.65);
  border: 1px stroke rgba(200, 180, 150, 0.3);
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
  backdrop-filter: blur(1px);
  z-index: 2;
}

.photo-frame {
  aspect-ratio: 3 / 4;
  overflow: hidden;
  background: #eee;
}

.photo-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-info {
  margin-top: 8px;
  text-align: center;
}

.handwritten-card-title {
  font-family: 'Caveat', cursive;
  font-size: 1.25rem;
  color: #3b2d26;
  margin: 0;
  line-height: 1.1;
}

.handwritten-date {
  font-family: 'Caveat', cursive;
  font-size: 0.95rem;
  color: #8c7365;
}

.page-number { font-family: 'Cinzel', serif; font-size: 0.68rem; color: #a89485; display: block; text-align: center; }
</style>