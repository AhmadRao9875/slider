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
        <div class="carousel-info">
          <div class="carousel-caption">
            <h5>{{ slide.title }}</h5>
            <p>{{ slide.text }}</p>
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

.carousel-info {
  position: absolute;
  top: 0;
  left: 25%;
  width: 50%;
  height: 100%;
}
.carousel-caption {
  width: 100%;
  left: 50%;
  top: 36.2%;
  transform: translate(-50%, -50%);
  position: absolute;
  text-align: center;
  color: #fff;
  display: flex;
  align-items: center;
  flex-direction: column;
}
.pagination-container {
  width: 114rem;
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
  width: 1.6rem;
  height: 1.6rem;
  border-radius: 50%;
  border: 1px solid #fff;
  background-color: transparent;
}
.dot {
  display: flex;
  width: 1rem;
  height: 1rem;
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
    width: 2rem;
    height: 2rem;
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
    top: 10%;
  }
  .carousel-caption {
    /* left: 23%; */
    top: 20%;
    padding: 7px;
    line-height: normal;
    margin: 0;
  }
  .dot-outer {
    width: 0.5rem;
    height: 0.5rem;
  }
  .dot {
    width: 0.5rem;
    height: 0.5rem;
  }
}
</style>
