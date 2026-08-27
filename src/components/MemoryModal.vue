<template>
  <Transition name="modal-fade">
    <div v-if="isOpen && memory" class="modal-overlay" @click.self="close">
      <div class="modal-content">
        <button class="close-btn" @click="close" aria-label="Đóng">✕</button>
        
        <div class="modal-body">
          <div class="modal-image-col">
            <img :src="resolveImageUrl(memory.photoUrl)" :alt="memory.title" />
          </div>

          <div class="modal-text-col">
            <span class="modal-date">🗓️ {{ memory.date }}</span>
            <h2 class="modal-title">{{ memory.title }}</h2>
            <p class="modal-desc">{{ memory.message }}</p>
            
            <div v-if="memory.letterToChild" class="letter-box">
              <span class="letter-tag">✉️ Lời ba mẹ nhắn gửi con:</span>
              <p class="letter-text">"{{ memory.letterToChild }}"</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  name: 'MemoryModal',
  props: {
    isOpen: Boolean,
    memory: Object
  },
  emits: ['close'],
  setup(props, { emit }) {
    const close = () => emit('close')

    const resolveImageUrl = (path) => {
      if (!path) return ''
      if (path.startsWith('http://') || path.startsWith('https://')) return path
      const baseUrl = import.meta.env.BASE_URL || '/'
      return `${baseUrl}${path.replace(/^\//, '')}`
    }

    return { close, resolveImageUrl }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&display=swap');

/* Hiệu ứng Fade Overlay */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

/* Modal Overlay */
.modal-overlay {
  position: fixed;
  inset: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(60, 45, 35, 0.5);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  padding: 16px;
  box-sizing: border-box;
}

/* Modal Container Main */
.modal-content {
  background: #fffdf9;
  max-width: 820px;
  width: 100%;
  max-height: 90vh;
  border-radius: 16px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(135, 105, 80, 0.25);
  border: 3px solid #f2e2d0;
  display: flex;
  flex-direction: column;
}

/* Nút Đóng Nổi Bật */
.close-btn {
  position: absolute;
  top: 12px;
  right: 12px;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: #f7e7ce;
  border: 1px solid #e8cca4;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  z-index: 10;
  color: #7a5843;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.close-btn:hover {
  background: #e8a87c;
  color: #ffffff;
  transform: scale(1.08);
}

/* Bố cục Grid 2 cột trên Desktop/Tablet */
.modal-body {
  display: grid;
  grid-template-columns: 1.1fr 1fr;
  max-height: 90vh;
  overflow-y: auto;
}

/* Cột Ảnh */
.modal-image-col {
  background: #f7f1e5;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  min-height: 250px;
}

.modal-image-col img {
  width: 100%;
  height: 100%;
  max-height: 70vh;
  object-fit: contain;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
}

/* Cột Nội Dung Văn Bản */
.modal-text-col {
  padding: 28px 24px 24px 24px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow-y: auto;
}

.modal-date {
  font-family: 'Cinzel', serif;
  font-size: 0.8rem;
  color: #b88b68;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.modal-title {
  font-family: 'Caveat', cursive;
  font-size: 2.2rem;
  color: #5c473a;
  margin: 4px 0 10px;
  line-height: 1.1;
}

.modal-desc {
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-size: 0.95rem;
  color: #6e584c;
  line-height: 1.6;
  margin-bottom: 16px;
}

/* Thư Nhắn Của Ba Mẹ */
.letter-box {
  background: #fcf4eb;
  border-left: 4px solid #e8a87c;
  border-radius: 0 10px 10px 0;
  padding: 14px 16px;
}

.letter-tag {
  font-size: 0.78rem;
  font-weight: 700;
  color: #c47347;
  display: block;
  margin-bottom: 4px;
}

.letter-text {
  font-family: 'Caveat', cursive;
  font-size: 1.25rem;
  color: #57443a;
  line-height: 1.35;
  margin: 0;
}

/* 📱 Responsive cho Mobile & Tablet dọc (Dưới 768px) */
@media (max-width: 768px) {
  .modal-overlay {
    padding: 10px;
  }

  .modal-content {
    max-height: 88vh;
    border-radius: 12px;
  }

  .modal-body {
    grid-template-columns: 1fr; /* Chuyển thành 1 cột dọc */
  }

  .modal-image-col {
    padding: 12px;
    max-height: 38vh;
  }

  .modal-image-col img {
    max-height: 35vh;
  }

  .modal-text-col {
    padding: 16px 18px 20px 18px;
  }

  .modal-title {
    font-size: 1.8rem;
  }

  .modal-desc {
    font-size: 0.9rem;
  }

  .letter-text {
    font-size: 1.15rem;
  }
}
</style>