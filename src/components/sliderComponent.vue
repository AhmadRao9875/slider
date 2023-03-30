<template>
  <div class="heading"><h1>This is Image slider</h1></div>
  <div class="carousel">
    <div class="carousel-inner">
      <transition-group name="slide" mode="out-in">
        <div
          class="carousel-item"
          :class="{ active: item === currentItem }"
          v-for="item in items"
          :key="item.id"
        >
          <img :src="item.image" alt="Carousel Item" />
          <div class="carousel-caption">
            <h3>{{ item.title }}</h3>
            <p>{{ item.description }}</p>
          </div>
        </div>
      </transition-group>
    </div>
    <div class="carousel-dots">
      <span
        class="dot"
        :class="{ active: item === currentItem }"
        v-for="item in items"
        :key="item.id"
        @click="setCurrentItem(item)"
      ></span>
    </div>
    <div class="icon-container">
      <div class="icon-centering-container" @click="prevItem()">
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
      <div class="icon-centering-container" @click="nextItem()">
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1,
          title: "First Item",
          description: "This is the first carousel item",
          image: "https://picsum.photos/id/1018/1200/800",
        },
        {
          id: 2,
          title: "Second Item",
          description: "This is the second carousel item",
          image: "https://picsum.photos/id/1015/1200/800",
        },
        {
          id: 3,
          title: "Third Item",
          description: "This is the third carousel item",
          image: "https://picsum.photos/id/1019/1200/800",
        },
      ],
      currentItem: null,
    };
  },
  mounted() {
    // displays the item 0 on the start,
    this.currentItem = this.items[0];
  },
  methods: {
    nextItem() {
      const currentIndex = this.items.indexOf(this.currentItem);
      console.log(currentIndex, "this is currentIndex");
      this.currentItem =
        // if the current item is the last item of the array ,it will set the currentItem to 0 else to the next
        currentIndex === this.items.length - 1
          ? this.items[0]
          : this.items[currentIndex + 1];
    },
    prevItem() {
      const currentIndex = this.items.indexOf(this.currentItem);
      this.currentItem =
        currentIndex === 0
          ? this.items[this.items.length - 1]
          : this.items[currentIndex - 1];
    },
    setCurrentItem(item) {
      // this will display the the item wchic is clicked
      this.currentItem = item;
    },
  },
};
</script>

<style>
.heading {
  display: flex;
  justify-content: center;
  background-color: antiquewhite;
}
.carousel {
  background-color: rgb(233, 231, 231);
  position: relative;
  margin: 0 auto;
  width: 100%;
  max-width: 75rem;
  height: 100%;
}

.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 100%;
  padding-bottom: 60%;
}

.carousel-item {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
}
.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-item.active {
  right: 0;
  opacity: 1;
  transition: opacity 1s ease-in-out;
}

.carousel-caption {
  position: absolute;
  bottom: 20%;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  color: #fff;
}

.carousel-caption h3 {
  font-size: 2rem;
  margin-bottom: 1.8rem;
}

.carousel-caption p {
  font-size: 1.8rem;
  line-height: 1.5;
}

.carousel-dots {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 90%;
  left: 50%;
}

.carousel-dots .dot {
  display: inline-block;
  width: 15px;
  height: 15px;
  margin: 0 5px;
  border-radius: 50%;
  background-color: #bbb;
  cursor: pointer;
}

.carousel-dots .dot.active {
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
.carousel-slide-enter-active {
  transition: all 0.5s ease;
}

.carousel-slide-enter {
  opacity: 0;
  transform: translateX(100%);
}

.carousel-slide-leave-active {
  transition: all 1s ease;
}

.carousel-slide-leave {
  opacity: 0;
  transform: translateX(-100%);
}

.slide-move {
  transition: transform 1s ease;
}

.slide-enter {
  transform: translateX(100%);
}

.slide-leave-to {
  transform: translateX(-100%);
}
</style>
