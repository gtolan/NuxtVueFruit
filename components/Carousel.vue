<template>
  <div class="row carousel-wrap">
    <header>
      <div class="welcome-text">
        <h1>Fruit & Vegetable Exporters</h1>
        <a class="learn" href="/about">Learn More</a>
      </div>
    </header>
    <div class="slider-btns">
      <button
        @click="prevSlide"
        class="btn-floating btn-medium waves-effect waves-light blue-grey lighten-3 left-chevron"
      >
        <span class="chevron">&lsaquo;</span>
      </button>
      <button
        @click="nextSlide"
        class="btn-floating btn-medium waves-effect waves-light blue-grey lighten-3 right-chevron"
      >
        <span class="chevron">&rsaquo;</span>
      </button>
    </div>

    <div
      class="slide video"
      v-for="slide in carousel"
      :key="slide.id"
      :class="{ active: (slide.id == activeSlide) }"
    >
      <video loop autoplay muted>
        <source :src="slide.mp4" type="video/mp4">
      </video>
    </div>

    <div class="row slider-control center-align">
      <button
        v-for="slide in carousel"
        :key="slide.id"
        class="btn-floating btn-small waves-effect waves-light white"
        @click="viewSlide(slide.id)"
        :class="{ active: (slide.id == activeSlide) }"
      >
        <div class="sphere"></div>
        <!-- <i class="material-icons">trip_origin</i> -->
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Carousel",
  data() {
    return {
      viewSlideInProgress: false,
      activeSlide: 1,
      autoSliding: true,
      carousel: [
        {
          id: 1,
          mp4: require("../assets/berries.mp4"),
          img: require("../assets/images/apple.jpg"),
          title: "Comfort",
          link: "products/all/nike",
          text: "Walk on clouds"
        },
        {
          id: 2,
          mp4: require("../assets/lebfarm.mp4"),
          img: require("../assets/images/oranges.jpg"),
          title: "Rain Ready",
          link: "products/all/adidas",
          text: "For all weather sneakers"
        },
        {
          id: 3,
          mp4: require("../assets/leboranges.mp4"),
          img: require("../assets/images/bananas.jpg"),
          title: "Ready for Anything",
          link: "products/all/nike",
          text: "The right shoe for the right moment"
        },
        {
          id: 4,
          mp4: require("../assets/lebfarm2.mp4"),
          img: require("../assets/images/grapes.png"),
          title: "adidas",
          link: "products/all/nike",
          text: "The best brands available"
        }
      ]
    };
  },
  methods: {
    nextSlide() {
      this.activeSlide >= this.carousel.length
        ? (this.activeSlide = 1)
        : this.activeSlide++;
    },
    prevSlide() {
      this.activeSlide === 1
        ? (this.activeSlide = this.carousel.length)
        : this.activeSlide--;
    },
    viewSlide(id) {
      this.activeSlide = id;
      this.viewSlideInProgress = true;
      let self = this;
      if (this.autoSliding == false) {
        setTimeout(() => {
          self.viewSlideInProgress = false;
          self.startSlider();
        }, 6000);
      }
    },
    startSlider() {
      let self = this;
      const runSlide = function(self) {
        setTimeout(() => {
          if (self.viewSlideInProgress == false) {
            self.nextSlide();
            runSlide(self);
          }
        }, 4500);
        self.autoSliding = false;
      };
      runSlide(self);
    }
  },
  computed: {
    activeSlideLink: function() {
      let index = Number.parseInt(this.activeSlide);
      index--;
      let link = this.carousel[index].link;
      return link;
    }
  },
  mounted() {
    this.startSlider();
  }
};
</script>

<style lang="scss" scoped>
.carousel-wrap {
  position: relative;
  width: 100vw;
  height: 90vh;
  margin-top: -75px;
  margin-bottom: 0px;
}
.carousel-wrap .slide {
  height: 100%;
  width: 100%;
  background-size: cover;
  background-position: center;
  position: absolute;
  opacity: 0;
  will-change: opacity;
  transition: 1s ease-in-out;
}
.carousel-wrap .slide.active {
  opacity: 1;
}
.carousel-wrap .slide h1 {
  margin-top: 4rem;
  padding-top: 34vh;
  color: white;
  font-weight: 600;
  padding-left: 0rem;
  text-align: center;
}
.carousel-wrap .slide h5 {
  margin-top: 0px;
  padding-top: 2vh;
  color: white;
  font-weight: 300;
  padding-left: 0rem;
  text-align: center;
}
.carousel-wrap .see-more {
  text-align: center;
  z-index: 10;
  position: absolute;
  width: 12rem;
  margin-left: calc(50vw - 6rem);
  top: 65vh;
}
.slider-btns {
  position: absolute;
  margin-top: 25vh;
  display: flex;
  width: 100vw;
  justify-content: space-between;
}
.slider-btns .left-chevron {
  z-index: 10;
  margin: 10px;
  text-shadow: -3px 1px 4px grey;
  border: none;
  transition: 0.4s ease-in;
  cursor: pointer;
  background-color: #d3d3d39c;
}
.slider-btns .right-chevron {
  z-index: 10;
  margin: 10px;
  text-shadow: 3px 1px 4px grey;
  border: none;
  transition: 0.4s ease-in;
  cursor: pointer;
  background-color: #d3d3d39c;
}
.slider-btns:hover .right-chevron,
.slider-btns:hover .left-chevron {
  transform: scale(1.2);
}
.slider-control {
  text-align: center;
  z-index: 4;
  position: absolute;
  width: 100vw;
  top: 80vh;
}
.slider-control button {
  margin: 0px 5px;
  transition: 0.3s ease-in-out;
  transform-origin: center;
  transform: scale(0.6);
  border-radius: 50%;
  height: 2.2rem;
  width: 2.2rem;
  padding: 0px;
}
button div.sphere {
  background-image: radial-gradient(#8bc34a 0%, #009688 20%, #4caf50 40%);
  background-color: transparent;
  border: none;
  height: 2rem;
  width: 2rem;
  border-radius: 50%;
}
.slider-control .btn-floating.active {
  background-color: lightslategray !important;
  transform: scale(1);
}
@media only screen and (max-width: 550px) {
  .carousel-wrap .slide h1 {
    margin-top: 0px;
    padding-top: 29vh;
  }
}
.slider img {
  width: 100%;
  position: absolute;
}
header {
  position: absolute;
  width: 100%;
  margin-top: 205px;
  z-index: 1;
}
.welcome-text h1 {
  text-align: center;
  background-color: #0000007a;
  background-image: linear-gradient(to right, #808080ba, black, #4c4b4b29);
  min-width: 400px;
  max-width: 600px;
  margin: auto;
  padding: 5px;
  color: white;
}
.welcome-text {
  top: 44%;
  position: absolute;
  width: 100%;

  h1 {
    color: white;
    text-align: center;
    font-weight: 100;
    margin-top: 0rem;
    font-size: calc(3.25rem + 6 * ((100vw - 320px) / 1080));
    font-family: "Playfair Display", serif;
    animation: 0.5s scaleIn ease-in-out;
    animation-fill-mode: forwards;
    overflow: hidden;
  }
}
a.learn {
  width: 12rem;
  position: relative;
  display: block;
  text-decoration: none;
  margin-top: 2rem;
  margin-left: calc(50vw - 6rem);
  text-align: center;
  border: 2px solid;
  padding: 10px;
  color: white;
  background-color: #0000005c;
  border-radius: 22px;
  font-family: sans-serif;
  letter-spacing: 1px;
}
.chevron {
  font-size: 5rem;
  line-height: 2rem;
  color: white;
}
video {
  min-height: 450px;
  width: 100vw;
  max-height: 900px;
}
@media only screen and (max-width: 992px) {
  video {
    min-height: 450px;
    width: auto;
    max-height: 616px;
  }
}
</style>