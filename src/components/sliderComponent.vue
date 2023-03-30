<template>
  <div class="carousel">
    <div
      class="carousel-inner"
      :style="{ transform: 'translateX(' + -currentIndex * 100 + '%)' }"
    >
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="carousel-item"
        :class="{ active: index === currentIndex }"
      >
        <img :src="slide.imageSrc" :alt="slide.imageAlt" />
        <div class="carousel-caption">
          <h5>{{ slide.title }}</h5>
          <p>{{ slide.text }}</p>
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
    <div class="carousel-dots">
      <span
        v-for="(slide, index) in slides"
        :key="index"
        class="carousel-dot"
        :class="{ active: index === currentIndex }"
        @click="goToSlide(index)"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
  overflow: hidden;
}

.carousel-inner {
  width: 100%;
  height: 100%;
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-item {
  flex-shrink: 0;
  position: relative;
  width: 100%;
}

.carousel-item img {
  width: 100%;
  max-height: 45rem;
}

.carousel-caption {
  position: absolute;
  top: 50%;
  left: 50%;
  padding: 15px;
  color: #fff;
}

.carousel-dots {
  position: absolute;
  display: flex;
  top: 95%;
  left: 50%;
  justify-content: center;
  /* margin-top: 10px; */
}

.carousel-dot {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: #bbb;
  margin: 0 5px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.carousel-dot.active {
  background-color: #fff;
  width: 10px;
  height: 10px;
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
  width: 1.8rem;
  height: 1.8rem;
  top: 50%;
  cursor: pointer;
  border: 1px solid black;
  stroke: black100;
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
</style>
