<template>
  <div class="carousel">
    <div class="slide">
      <div class="icon-container">
        <div class="icon-centering-container" @click="nextSlide()">
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
        <div class="icon-centering-container" @click="prevSlide()">
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
      <transition name="fade">
        <img :src="slides[currentSlide].image" alt="" />
      </transition>
      <div class="slide-text">{{ slides[currentSlide].text }}</div>
    </div>
    <!-- <button class="next-btn" @click="nextSlide">&#10095;</button> -->
    <div class="dots">
      <span
        v-for="(slide, index) in slides"
        :key="index"
        :class="{
          active: index === currentSlide,
          inactive: index !== currentSlide,
        }"
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
          image: require("@/assets/image1.jpg"),
          text: "Slide 1 text",
        },
        {
          image: require("@/assets/image2.jpg"),
          text: "Slide 2 text",
        },
        {
          image: require("@/assets/image3.jpg"),
          text: "Slide 3 text",
        },
      ],
      currentSlide: 0,
    };
  },
  // mounted() {
  //   this.nextSlide();
  // },
  methods: {
    nextSlide() {
      this.currentSlide++;
      if (this.currentSlide >= this.slides.length) {
        this.currentSlide = 0;
      }
    },
    prevSlide() {
      this.currentSlide--;
      if (this.currentSlide < 0) {
        this.currentSlide = this.slides.length - 1;
      }
    },
    goToSlide(index) {
      this.currentSlide = index;
    },
  },
};
</script>

<style>
.carousel {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 74.46rem;
}

.prev-btn,
.next-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
  cursor: pointer;
  font-size: 2em;
}

.prev-btn {
  left: 0;
}

.next-btn {
  right: 0;
}

.slide {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background-size: cover;
  background-position: center;
  transition: transform 5s ease;
  transform: translateX(0);
  position: relative;
}
.slide img {
  width: 100%;
  min-height: 93rem;
  object-fit: cover;
}
.slide.next {
  transform: translateX(100%);
  transition: transform 0.5s ease;
}

.slide.prev {
  transform: translateX(-100%);
}
.active {
  opacity: 1;
  z-index: 1;
}

.inactive {
  opacity: 0.5;
  z-index: 0;
}

.slide-text {
  position: absolute;
  top: 50%;
  left: 50%;
  max-width: 100%;
  padding: 1em;
  background-color: rgba(0, 0, 0, 0.5);
  color: #fff;
  text-align: center;
  font-size: 1.2em;
  transition: opacity 0.5s ease;
  opacity: 1;
}

.dots {
  display: flex;
  position: absolute;
  justify-content: center;
  margin-top: 1em;
  top: 80%;
}

.dots span {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background-color: #f8f6f6;
  margin: 0 5px;
  cursor: pointer;
  transition: background-color 0.5s ease;
}

.dots span.active {
  background-color: #0d0d0d;
  height: 15px;
  width: 15px;
}

.icon-container {
  width: 90%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.icon {
  position: absolute;
  width: 2.8rem;
  height: 2.8rem;
  top: 50%;
  cursor: pointer;
  border: 1px solid rgb(249, 247, 247);
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

.icon-centering-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
