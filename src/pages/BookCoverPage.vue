<template>
  <!-- Trang Bìa Trái (Inside Front Cover) -->
  <div class="book-page cover-inside-left">
    <div class="inside-border">
      <div class="vintage-stamp">
        <span class="stamp-year">2026</span>
        <span class="stamp-text">LIMITED EDITION</span>
      </div>

      <div class="welcome-message">
        <h3 class="handwritten-subtitle">Gửi Bé Mầm Thân Yêu,</h3>
        <p class="handwritten-body">
          Mỗi khoảnh khắc con lớn lên đều là một điều kỳ diệu. Cuốn nhật ký này lưu giữ từng nụ cười, bước chân và kỷ niệm ngọt ngào nhất của gia đình mình.
        </p>
      </div>

      <div class="wax-seal-container">
        <div class="wax-seal">
          <span class="seal-inner">FAMILY</span>
        </div>
      </div>

      <div class="footer-note">
        <span>Ghi chép bởi Ba & Mẹ</span>
      </div>
    </div>
  </div>

  <!-- Trang Bìa Phải (Main Cover) -->
  <div class="book-page cover-page">
    <div class="book-spine-line"></div>
    <div class="corner-ornament top-left">꧁</div>
    <div class="corner-ornament top-right">꧂</div>
    <div class="corner-ornament bottom-left">꧁</div>
    <div class="corner-ornament bottom-right">꧂</div>

    <div class="page-border">
      <div class="header-badge">
        <span class="star-icon">✦</span>
        <span class="sub-heading">MEMORIES & JOURNEY</span>
        <span class="star-icon">✦</span>
      </div>
      
      <div class="title-container">
        <span class="vintage-divider">❖</span>
        <h1 class="main-title">Hành Trình Khôn Lớn Của {{ childName || 'Bé Mầm' }}</h1>
        <span class="vintage-divider">❖</span>
      </div>
      
      <p class="quote">
        "Cuốn sách này lưu giữ từng tiếng khóc chào đời, bước chân đầu tiên và hành trình ngập tràn tình yêu mà gia đình mình cùng tạo nên."
      </p>

      <div class="gift-footer">
        <span class="gift-decor">꧁</span>
        <span class="gift-text">Món quà ba mẹ dành cho con</span>
        <span class="gift-decor">꧂</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookCoverPage',
  props: { childName: String }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Cormorant+Garamond:ital,wght@0,600;1,400&display=swap');

/* Trang bìa trái - Màu kem hồng đào dịu ấm */
.cover-inside-left {
  background: #fbf2e9;
  padding: 22px;
  height: 100%;
  box-sizing: border-box;
}

.inside-border {
  border: 2px dashed #e8d0bc;
  border-radius: 8px;
  height: 100%;
  padding: 24px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  text-align: center;
  background: #ffffff;
  box-shadow: inset 0 0 15px rgba(247, 231, 206, 0.4);
}

.vintage-stamp {
  border: 1.5px solid #dcbfa6;
  background: #fff8f0;
  padding: 4px 14px;
  border-radius: 6px;
  transform: rotate(-2deg);
}
.stamp-year { font-weight: bold; color: #b88b68; display: block; font-size: 0.82rem; }
.stamp-text { font-size: 0.62rem; letter-spacing: 1px; color: #caa485; }

.handwritten-subtitle {
  font-family: 'Caveat', cursive;
  font-size: 2rem;
  color: #7a5843;
  margin: 0 0 10px 0;
}

.handwritten-body {
  font-family: 'Caveat', cursive;
  font-size: 1.45rem;
  color: #8c6e5a;
  line-height: 1.45;
}

/* Thay dấu niêm phong màu đỏ sẫm thành huy hiệu đáng yêu */
.wax-seal {
  width: 62px;
  height: 62px;
  background: #e8a87c; /* Màu cam đào ấm */
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: inset 0 0 6px rgba(255,255,255,0.6), 0 4px 12px rgba(232, 168, 124, 0.35);
  border: 3px solid #f7cdac;
}
.seal-inner {
  color: #ffffff;
  font-family: 'Cinzel', serif;
  font-size: 0.65rem;
  font-weight: bold;
  letter-spacing: 1.5px;
}

.footer-note {
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  font-size: 0.95rem;
  color: #a38875;
}

/* Trang Bìa Phải */
.cover-page {
  background: #fffbf7;
  padding: 22px;
  height: 100%;
  box-sizing: border-box;
  position: relative;
}

.book-spine-line {
  position: absolute;
  top: 0; bottom: 0; left: 0;
  width: 10px;
  background: linear-gradient(to right, rgba(200, 175, 150, 0.2), transparent);
}

.corner-ornament { position: absolute; font-size: 1.3rem; color: #dcba96; opacity: 0.8; }
.top-left { top: 12px; left: 22px; }
.top-right { top: 12px; right: 14px; }
.bottom-left { bottom: 12px; left: 22px; }
.bottom-right { bottom: 12px; right: 14px; }

.page-border {
  border: 2px double #e8d5c4;
  border-radius: 8px;
  height: 100%;
  padding: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  box-sizing: border-box;
}

.sub-heading { font-family: 'Cinzel', serif; font-size: 0.7rem; letter-spacing: 2px; color: #c49a78; font-weight: 700; }
.main-title { font-family: 'Dancing Script', cursive; font-size: 2.7rem; color: #6e4e3a; margin: 8px 0; }
.quote { font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 1.1rem; color: #8a6f5c; line-height: 1.55; }
.gift-text { font-family: 'Cormorant Garamond', serif; font-size: 1.05rem; color: #b88b68; font-weight: 600; }
</style>