<template>
  <div class="carousel">
    <div class="carousel-inner" ref="slideArea">
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="slides"
        :class="index === currentIndex ? 'acitve-slide' : ''"
      >
        <div class="slide-box">
          <div
            class="slide-info"
            :style="{
              width: '100%',
              backgroundImage: `url(${slide.imageSrc})`,
              backgroundSize: 'cover',
              objectFit: 'cover',
            }"
          >
            <div class="information">
              <p class="title">{{ slide.title }}</p>
              <p class="description">{{ slide.text }}</p>
            </div>
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
      imagePath: require("@/assets/image2.jpg"),
      slides: [
        {
          imageSrc: "https://picsum.photos/id/1015/1200/800",
          imageAlt: "Image 1",
          title: "Nie wieder Decken streichen",
          text: "✓ 10 Jahre Garantie* ✓ geniale Preise ✓ schnelle Preisauskunft ✓ direkt vom Hersteller ✓ bis zu 30% sparen ✓ Top Qualität ✓ keine versteckte Kosten ✓ kurze Lieferzeiten",
        },
        {
          imageSrc: "https://picsum.photos/id/1018/1200/800",
          imageAlt: "Image 2",
          title: "Nie wieder Decken streichen",
          text: "✓ 10 Jahre Garantie* ✓ geniale Preise ✓ schnelle Preisauskunft ✓ direkt vom Hersteller ✓ bis zu 30% sparen ✓ Top Qualität ✓ keine versteckte Kosten ✓ kurze Lieferzeiten",
        },
        {
          imageSrc: "https://picsum.photos/id/1019/1200/800",
          imageAlt: "Image 3",
          title: "Nie wieder Decken streichen",
          text: "✓ 10 Jahre Garantie* ✓ geniale Preise ✓ schnelle Preisauskunft ✓ direkt vom Hersteller ✓ bis zu 30% sparen ✓ Top Qualität ✓ keine versteckte Kosten ✓ kurze Lieferzeiten",
        },
      ],
      currentIndex: 0,
      slideWidth: 0,
    };
  },
  mounted() {
    this.slideWidth = 300 / this.slides.length;
    this.$refs.slideArea.style.transform = "translateX(-0%)";
  },
  methods: {
    nextSlide() {
      if (this.currentIndex < this.slides.length - 1) {
        this.currentIndex++;
      } else {
        this.currentIndex = 0;
      }
      const nextSlideIndex = this.currentIndex * this.slideWidth;
      this.$refs.slideArea.style.transform = `translateX(-${nextSlideIndex}%)`;
    },
    prevSlide() {
      if (this.currentIndex > 0) {
        console.log(this.currentIndex, "this is prev ");
        this.currentIndex--;
        // const nextSlideIndex = this.currentIndex * this.slideWidth;
        this.$refs.slideArea.style.transform = `translateX(-${this.currentIndex}00%)`;
      }
      // this.currentIndex =
      //   (this.currentIndex - 1 + this.slides.length) % this.slides.length;
    },
    goToSlide(index) {
      this.currentIndex = index;
      this.$refs.slideArea.style.transform = `translateX(-${index}00%)`;
    },
  },
};
</script>

<style scoped>
p {
  margin: 0;
}

.carousel {
  position: relative;
  width: 100%;
  display: flex;
  height: 100%;
  overflow: hidden;
}

.carousel-inner {
  display: flex;
  height: 100%;
  width: 100%;
  /* transform: translateX(-30%); */
  transition: all 0.5s ease-out;
}
/* .carousel-inner img {
  width: 100%;
  height: 100%;
  object-fit: cover;
} */
.slides {
  flex: 0 0 calc(100% / 1);
  position: relative;
  width: 100%;
  height: auto;
  cursor: pointer;
}
.acitve-slide {
  /* opacity: 1; */
}
/* .active-next {
  transform: translateX(100%);
} */
.slide-box {
  width: 100%;
  height: 100%;

  /* display: flex; */
  justify-content: center;
  /* margin-top: 18.75rem; */
}

.slide-info {
  width: 100%;
  background-size: cover;
  background-position: center;
  overflow-x: hidden;
  text-align: center;
  height: 100vh;
}

.information {
  padding-top: 7.5rem;
}
.title {
  display: block;
  text-align: center;
  font-size: 2.875rem;
  color: #37474f;
  font-weight: bold;
  line-height: 1.22;
}
.description {
  display: block;
  font-size: 0.8125rem;
  color: #fff;
  font-weight: bold;
  text-align: center;
  line-height: 1.85;
  padding: 0 27.8rem 0 27.8rem;
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
  /* width: 1.125rem;
  height: 1.125rem; */
  width: 8px;
  height: 8px;
  border-radius: 50%;
  border: 1px solid #fff;
  background-color: transparent;
}
.dot {
  display: flex;
  /* width: 0.625rem;
  height: 0.625rem; */
  width: 8px;
  height: 8px;
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
  border: 1px solid rgb(253, 253, 253);
  stroke: rgb(253, 253, 253);
  border-radius: 50%;
  padding: 0.7rem;
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
  .description{
    padding: 0 10.5rem 0 10.5rem;
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
  .information {
    padding: 4.875rem 1rem 0 1rem;
  }
  .slide-info {
    padding-right: 2rem;
    /* padding-left: 2rem; */
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
    font-family: sans-serif ;
  }
  .description {
    color: white;
    font-size: 0.75rem;
    font-weight: normal;
    line-height: 1.3;
    padding: 0;
  }
  .icon-container {
    display: none;
  }
}
</style>
