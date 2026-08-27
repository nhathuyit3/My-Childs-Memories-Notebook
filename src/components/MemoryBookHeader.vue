<template>
  <header class="memory-header">
    <div class="header-paper">
      <div class="header-badge">
        <span class="star-icon">✨</span>
        <span class="sub-heading">BABY'S GROWTH JOURNAL</span>
        <span class="star-icon">✨</span>
      </div>
      
      <h1 class="main-title">Hành Trình Khôn Lớn Của {{ childInfo.name || 'Con' }}</h1>
      
      <p class="quote">
        "Cuốn sách này lưu giữ từng tiếng khóc chào đời, bước chân đầu tiên và hành trình ngập tràn tình yêu mà gia đình mình cùng tạo nên."
      </p>
      
      <div class="journal-seal">
        <span class="seal-line"></span>
        <span class="seal-icon">🧸</span>
        <span class="seal-line"></span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'MemoryBookHeader',
  props: {
    childInfo: {
      type: Object,
      default: () => ({})
    }
  }
}
</script>

<style scoped>
.memory-header {
  padding: 60px 20px 30px;
  display: flex;
  justify-content: center;
}

.header-paper {
  background: #ffffff;
  border: 1px solid #e8dfd1;
  padding: 40px 30px;
  max-width: 750px;
  width: 100%;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(184, 161, 131, 0.12);
  text-align: center;
  position: relative;
}

.header-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 12px;
}

.sub-heading {
  font-family: 'Cinzel', serif;
  font-size: 0.75rem;
  letter-spacing: 3px;
  color: #b08d57;
  font-weight: 700;
}

.star-icon {
  font-size: 0.8rem;
}

.main-title {
  font-family: 'Dancing Script', cursive;
  font-size: 3.8rem;
  color: #5c4338;
  margin: 5px 0 15px;
  line-height: 1.1;
}

.quote {
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  font-size: 1.25rem;
  color: #736154;
  line-height: 1.6;
  max-width: 580px;
  margin: 0 auto;
}

.journal-seal {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  margin-top: 25px;
}

.seal-line {
  height: 1px;
  width: 60px;
  background: #e2d3c1;
}

.seal-icon {
  font-size: 1.2rem;
}

@media (max-width: 576px) {
  .main-title {
    font-size: 2.8rem;
  }
  .quote {
    font-size: 1.1rem;
  }
}
</style>