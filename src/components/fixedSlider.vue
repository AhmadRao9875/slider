<template>
  <div class="carousel">
    <div
      class="carousel-inner"
      :style="{
        backgroundImage: `url(${imagePath})`,
        backgroundSize: 'cover',
        objectFit: 'cover',
      }"
    >
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="carousel-item"
        :class="index === currentIndex ? 'acitve-slide' : ''"
      >
        <div class="caption-box">
          <div class="carousel-info">
            <p class="title">{{ slide.title }}</p>
            <p class="description">{{ slide.text }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="icon-container">
      <div class="icon-centering-container" @click="prevSlide()">
        <svg
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="icon--left icon"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15.75 19.5L8.25 12l7.5-7.5"
          />
        </svg>
      </div>
      <div class="icon-centering-container" @click="nextSlide()">
        <svg
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="icon--right icon"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M8.25 4.5l7.5 7.5-7.5 7.5"
          />
        </svg>
      </div>
    </div>
    <div class="pagination-container">
      <div class="pagination">
        <span
          v-for="(slide, index) in slides"
          :key="index"
          class="dot-outer"
          @click="goToSlide(index)"
        >
          <span :class="{ active: index === currentIndex }" class="dot"></span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "fixedSlider",
  data() {
    return {
      imagePath: require("@/assets/image1.jpg"),
      slides: [
        {
          imageSrc: "https://picsum.photos/id/1015/1200/800",
          imageAlt: "Image 1",
          title: "Slide 1",
          text: "This is the text for slide 1",
        },
        {
          imageSrc: "https://picsum.photos/id/1018/1200/800",
          imageAlt: "Image 2",
          title: "Slide 2",
          text: "This is the text for slide 2",
        },
        {
          imageSrc: "https://picsum.photos/id/1019/1200/800",
          imageAlt: "Image 3",
          title: "Slide 3",
          text: "This is the text for slide 3",
        },
      ],
      currentIndex: 0,
    };
  },
  methods: {
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
    },
    prevSlide() {
      this.currentIndex =
        (this.currentIndex - 1 + this.slides.length) % this.slides.length;
    },
    goToSlide(index) {
      this.currentIndex = index;
    },
  },
};
</script>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  max-height: 74.46rem;
}

.carousel-inner {
  width: 100%;
  height: 90vh;
  position: relative;
  overflow: hidden;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}
.carousel-inner img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.carousel-item {
  width: 100%;
  height: 100%;
  opacity: 0;
  display: none;
  justify-content: center;
  align-content: center;
  align-items: center;
  transform: scale(0.8);
}
.acitve-slide {
  transform: scale(1);
  display: flex;
  right: 0;
  opacity: 1;
  animation: fadeInLeftToRight 1s ease-in-out;
}
.caption-box {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
}

.carousel-info {
  width: 100%;
  width: 50rem;
  text-align: center;
  margin-top: 18.75rem;
}

.title {
  display: block;
  font-size: 2.875rem;
  color: #37474f;
  font-weight: bold;
}
.description {
  font-size: 0.8rem;
  color: #fff;
  font-weight: 600;
  display: block;
  line-height: 1.85;
}
.pagination-container {
  width: 100%;
  position: absolute;
  left: 50%;
  top: 90%;
  transform: translate(-50%, -50%);
}
.pagination {
  display: flex;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  gap: 1.6rem;
}
.dot-outer {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  width: 1.125rem;
  height: 1.125rem;
  border-radius: 50%;
  border: 1px solid #fff;
  background-color: transparent;
}
.dot {
  display: flex;
  width: 0.6rem;
  height: 0.6rem;
  border-radius: 50%;
  background-color: transparent;
}

.active {
  background-color: #fff;
  border-color: #fff;
}
.icon-container {
  width: 90%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.icon-centering-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.icon {
  position: absolute;
  width: 3rem;
  height: 3rem;
  top: 50%;
  cursor: pointer;
  border: 1px solid rgb(254, 253, 253);
  stroke: rgb(248, 245, 245);
  border-radius: 50%;
  padding: 1.2rem;
}
.icon--right {
  right: 0;
  transform: translate(50%, -50%);
}
.icon--left {
  left: 0;
  transform: translate(-50%, -50%);
}

/* MEDIA QUERY */

@media only screen and (max-width: 1200px) {
  .dot-outer {
    width: 0.625rem;
    height: 0.625rem;
  }
  .icon-container {
    width: 85%;
  }
}
@media only screen and (max-width: 600px) {
  .icon {
    width: 1rem;
    height: 1rem;
    padding: 0.5rem;
  }
  .icon-container {
    width: 80%;
  }
  .carousel-info {
    margin-top: 4.8rem;
    padding-right: 2rem;
    padding-left: 2rem;
  }
  .dot-outer {
    width: 8px;
    height: 8px;
  }

  .title {
    font-size: 2.25rem;
    color: white;
    line-height: 1.3;
    font-weight: bold;
  }
  .description {
    color: white;
    font-size: 0.75rem;
    font-weight: normal;
    line-height: 1.3;
  }
  .icon-container {
    display: none;
  }
}
</style>
