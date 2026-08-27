<template>
  <div class="memory-card" @click="$emit('open-modal', memory)">
    <!-- Miếng băng dính dán ảnh trang trí -->
    <div class="washi-tape"></div>

    <div class="polaroid-wrapper">
      <div class="image-box">
        <img :src="resolveImageUrl(memory.photoUrl)" :alt="memory.title" loading="lazy" />
        <span class="date-badge">{{ memory.date }}</span>
      </div>

      <div class="polaroid-info">
        <h3 class="memory-title">{{ memory.title }}</h3>
        <p class="memory-message">{{ memory.message }}</p>
        <span class="read-more">✉ Xem nhật ký của con ➔</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoryCard',
  props: {
    memory: {
      type: Object,
      required: true
    }
  },
  emits: ['open-modal'],
  setup() {
    const resolveImageUrl = (path) => {
      if (!path) return ''
      if (path.startsWith('http://') || path.startsWith('https://')) return path
      const baseUrl = import.meta.env.BASE_URL
      return `${baseUrl}${path.replace(/^\//, '')}`
    }

    return { resolveImageUrl }
  }
}
</script>

<style scoped>
.memory-card {
  position: relative;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.memory-card:hover {
  transform: translateY(-6px) rotate(-1deg);
}

.washi-tape {
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 90px;
  height: 22px;
  background-color: rgba(235, 218, 193, 0.7);
  border: 1px dashed rgba(184, 161, 131, 0.5);
  z-index: 5;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.polaroid-wrapper {
  background: #ffffff;
  padding: 16px 16px 20px 16px;
  border-radius: 4px;
  box-shadow: 0 8px 20px rgba(168, 149, 126, 0.12);
  border: 1px solid #f2e9dc;
}

.image-box {
  position: relative;
  width: 100%;
  height: 250px;
  overflow: hidden;
  border-radius: 3px;
  background-color: #fcf9f5;
}

.image-box img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.date-badge {
  position: absolute;
  bottom: 8px;
  right: 8px;
  background: rgba(255, 255, 255, 0.92);
  padding: 3px 8px;
  font-family: 'Cinzel', serif;
  font-size: 0.72rem;
  font-weight: 600;
  color: #70584c;
  border-radius: 2px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.08);
}

.polaroid-info {
  margin-top: 15px;
  text-align: left;
}

.memory-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.35rem;
  font-weight: 600;
  color: #4a3a31;
  margin-bottom: 6px;
}

.memory-message {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-size: 0.85rem;
  color: #78685d;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.read-more {
  display: inline-block;
  margin-top: 10px;
  font-family: 'Dancing Script', cursive;
  font-size: 1.15rem;
  color: #b08d57;
  font-weight: 700;
}
</style>