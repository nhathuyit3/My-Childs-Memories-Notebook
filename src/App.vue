<template>
  <div id="memory-book-app">
    <div class="book-viewport">
      <button class="nav-arrow prev-arrow" @click="flipPrev" :disabled="currentPage === 0">❮</button>

      <div class="book-wrapper">
        <div class="book-container" ref="bookElement">
          <BookCoverPage :childName="bookData.childInfo.name" />
          <BookTOCPage :milestones="bookData.milestones" @go-to-page="handleGoToPage" />
          <BookStagePage
            v-for="(stage, index) in bookData.milestones"
            :key="stage.id"
            :stage="stage"
            :stageIndex="index"
            @open-modal="handleOpenModal"
          />
        </div>
      </div>

      <button class="nav-arrow next-arrow" @click="flipNext" :disabled="currentPage >= totalPages - 1">❯</button>
    </div>

    <MemoryModal :isOpen="isModalOpen" :memory="selectedMemory" @close="isModalOpen = false" />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { PageFlip } from 'page-flip'
import BookCoverPage from './pages/BookCoverPage.vue'
import BookTOCPage from './pages/BookTOCPage.vue'
import BookStagePage from './pages/BookStagePage.vue'
import MemoryModal from './components/MemoryModal.vue'

export default {
  name: 'App',
  components: { BookCoverPage, BookTOCPage, BookStagePage, MemoryModal },
  setup() {
    const bookData = ref({ childInfo: {}, milestones: [] })
    const isModalOpen = ref(false)
    const selectedMemory = ref(null)
    const bookElement = ref(null)
    const pageFlip = ref(null)
    const currentPage = ref(0)
    const totalPages = ref(0)

    // Tính toán chiều cao/rộng tối ưu để sách phủ 88-92% màn hình thiết bị
    const calculateBookDimensions = () => {
      const screenWidth = window.innerWidth
      const screenHeight = window.innerHeight
      const isMobile = screenWidth <= 768

      // Chiều cao sách chiếm 88% màn hình
      const bookHeight = Math.round(screenHeight * 0.88)
      
      // Tỉ lệ 1 trang sách chuẩn (Rộng = 0.72 x Cao)
      const bookWidth = isMobile 
        ? Math.round(screenWidth * 0.92)
        : Math.round(bookHeight * 0.72)

      return { width: bookWidth, height: bookHeight, isMobile }
    }

    const initBookFlip = () => {
      if (!bookElement.value) return
      const { width, height, isMobile } = calculateBookDimensions()

      pageFlip.value = new PageFlip(bookElement.value, {
        width: width,
        height: height,
        size: 'fixed',
        minWidth: 280,
        maxWidth: 700,
        minHeight: 400,
        maxHeight: 950,
        maxShadowOpacity: 0.35,
        showCover: true,
        usePortrait: isMobile,
        
        // 🛑 VÔ HIỆU HÓA TOÀN BỘ THAO TÁC CHUỘT / KÉO / CLIK TRÊN TRANG SÁCH
        clickEvent: false,             // Tắt click mép trang
        disableFlipByClick: true,      // Tắt hoàn toàn sự kiện lật bằng click chuột
        swipeDistance: 0,              // Tắt khoảng cách vuốt/kéo trang
        mobileScrollSupport: false     // Tắt bắt sự kiện cuộn/kéo trên di động
      })

      const pages = bookElement.value.querySelectorAll('.book-page')
      pageFlip.value.loadFromHTML(pages)
      totalPages.value = pages.length

      pageFlip.value.on('flip', (e) => {
        currentPage.value = e.data
      })
    }

    const handleResize = () => {
      if (pageFlip.value) {
        const { width, height } = calculateBookDimensions()
        pageFlip.value.update({ width, height })
      }
    }

    onMounted(async () => {
      try {
        const module = await import('./data/memories.json')
        bookData.value = module.default
        await nextTick()
        initBookFlip()
        window.addEventListener('resize', handleResize)
      } catch (error) {
        console.error('Lỗi khi tải dữ liệu sách:', error)
      }
    })

    onUnmounted(() => window.removeEventListener('resize', handleResize))

    const flipPrev = () => pageFlip.value?.flipPrev()
    const flipNext = () => pageFlip.value?.flipNext()
    const handleGoToPage = (pageIndex) => pageFlip.value?.flip(pageIndex)
    const handleOpenModal = (memory) => {
      selectedMemory.value = memory
      isModalOpen.value = true
    }

    return {
      bookData, isModalOpen, selectedMemory, bookElement,
      currentPage, totalPages, flipPrev, flipNext, handleGoToPage, handleOpenModal
    }
  }
}
</script>

<style>
body {
  margin: 0;
  /* Nền kem sữa ấm áp với họa tiết chấm bi tròn pastel trẻ thơ */
  background-color: #fdf6ed;
  background-image: 
    radial-gradient(#f0decb 2px, transparent 2px),
    radial-gradient(circle at center, rgba(255, 255, 255, 0.8) 0%, rgba(253, 246, 237, 0.95) 100%);
  background-size: 24px 24px, 100% 100%;
  font-family: 'Plus Jakarta Sans', sans-serif;
  color: #5c473a;
  overflow: hidden;
}

.book-viewport {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  box-sizing: border-box;
  position: relative;
}

/* Khung sách được làm nổi bật bằng bóng đổ mềm pastel */
.book-wrapper {
  padding: 10px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 12px;
  box-shadow: 
    0 20px 40px rgba(181, 148, 123, 0.18),
    0 0 35px rgba(255, 238, 217, 0.8);
}

/* Nút lật trang tone Pastel dịu ngọt */
.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: #ffffff;
  border: 2px solid #f2e2d0;
  color: #8c6e58;
  font-size: 1.2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 6px 18px rgba(181, 148, 123, 0.15);
  transition: all 0.25s ease;
  z-index: 20;
}

.nav-arrow:hover:not(:disabled) {
  background: #f7e7ce;
  color: #5c473a;
  border-color: #e8cca4;
  transform: translateY(-50%) scale(1.08);
}

.nav-arrow:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.prev-arrow { left: 28px; }
.next-arrow { right: 28px; }

@media (max-width: 768px) {
  .nav-arrow {
    width: 40px;
    height: 40px;
    bottom: 15px;
    top: auto;
    transform: none;
  }
  .prev-arrow { left: 20%; }
  .next-arrow { right: 20%; }
}
</style>