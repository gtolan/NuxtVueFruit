<template>
  <div>
    <section id="tagLine">
      <h1>We are devoted to our mission of supplying you with the finest and freshest Lebanese products</h1>
    </section>
    <section id="ourWork" ref="ourWork">
      <h1>
        Our Products
        <span class="bottom-border" ref="borderBottom"></span>
      </h1>

      <div class="tab" ref="tabOne">
        <a class="jump" href="/products/fruit">
          <h1>Fruit</h1>
          <p>Harvest</p>
        </a>
      </div>

      <div class="tab" ref="tabTwo">
        <a class="jump" href="/products/vegetables">
          <h1>Vegetables</h1>
          <p>Harvest</p>
        </a>
      </div>

      <div class="tab" ref="tabThree">
        <a class="jump" href="/products">
          <h1>Harvest</h1>
          <p>by Country</p>
        </a>
      </div>

      <div class="tab" ref="tabFour">
        <a class="jump" href="/products/calendar">
          <h1>Whats in Season</h1>
          <p>Calendar</p>
        </a>
      </div>
      <product-slider/>
    </section>
    <section id="services">
      <h1>We are the center for storing packing and sending the fresh</h1>
      <p>
        We have state of the art cooling rooms to ensure imported and goods for export are kept in the safest and
        healthiest ways possible.
        We will stay in touch with our deliveries to maintain high quality and customer service
      </p>
      <a>View our services</a>
    </section>
    <NewsSection/>

    <section id="workWithUs">
      <h1>Let's start working together</h1>
      <a href="/contact">Get in Touch</a>
    </section>
  </div>
</template>

 <script>
// import EventBus from "../eventBus";
import ProductSlider from "./ProductSlider.vue";
import NewsSection from "./NewsSection.vue";

export default {
  name: "Homepage",
  components: { ProductSlider, NewsSection },
  data() {
    return {
      observer: null,
      options: {
        root: null,
        rootMargin: "0px",
        // threshold: .5
        threshold: this.buildThresholdList()
      }
    };
  },
  methods: {
    buildThresholdList() {
      let thresholds = [];
      let numSteps = 10;

      for (let i = 1.0; i <= numSteps; i++) {
        let ratio = i / numSteps;
        thresholds.push(ratio);
      }

      thresholds.push(0);
      return thresholds;
    },
    handleIntersect(entries, observer) {
      this.observer = observer;
      const tabs = [
        this.$refs.tabOne,
        this.$refs.tabTwo,
        this.$refs.tabThree,
        this.$refs.tabFour
      ];
      entries.forEach(entry => {
        // console.log(entry.target, "entry");

        if (
          entry.intersectionRatio < 0.2 &&
          entry.target.classList.contains("bottom-border")
        ) {
          entry.target.classList.remove("anim-border");
        } else if (
          entry.intersectionRatio > 0.9 &&
          entry.target.classList.contains("bottom-border")
        ) {
          entry.target.classList.add("anim-border");
        }

        if (entry.intersectionRatio > 0.15 && entry.target.id == "ourWork") {
          console.log(
            entry.isIntersecting,
            entry.intersectionRatio,
            "inter-ourWrk",
            entry.target
          );
          // entry.target.classList.add('returnPos')
          console.log(tabs, "tabrefs");
          for (var i = 0; i < tabs.length; i++) {
            var tab = tabs[i];
            tab.classList.add("returnPos");
          }

          //entry.target.style.backgroundColor = increasingColor.replace("ratio", entry.intersectionRatio);
        } else if (
          entry.intersectionRatio < 0.15 &&
          entry.target.id == "ourWork"
        ) {
          console.log(
            entry.isIntersecting,
            entry.intersectionRatio,
            "inter",
            entry.target,
            tabs
          );
          // entry.target.classList.remove('returnPos')
          for (var i = 0; i < tabs.length; i++) {
            var tab = tabs[i];
            tab.classList.remove("returnPos");
            tab.classList.add("test-returnPos");
          }
        }
      });
    }
  },
  mounted() {
    this.observer = new IntersectionObserver(
      this.handleIntersect,
      this.options
    );
    let els = [this.$refs.ourWork, this.$refs.borderBottom];
    els.forEach(el => {
      this.observer.observe(el);
    });
  }
};
</script>

<style lang="scss" scoped>
section#ourWork {
  text-align: center;
  .tab {
    background: rgba(252, 90, 93, 0.9);
    color: white;
    display: inline-block;
    text-align: center;
    width: 40%;
    margin: 0.5rem;
    min-height: 40vh;
    background-size: cover;
    background-repeat: no-repeat;
    cursor: pointer;
    transition: 0.4s ease-in-out;
    vertical-align: top;
    overflow: hidden;
    a.jump {
      display: contents;
      margin: 0px;
      display: block;
      width: 100%;
      height: auto;
      min-height: 40vh;
      background-color: rgba(255, 0, 0, 0.14);
    }
  }
  .tab:hover a.jump {
    background-color: #ff000087;
  }

  .tab:nth-child(2) {
    background: linear-gradient(rgba(255, 0, 0, 0), rgba(255, 0, 0, 0)),
      url(../assets/images/fruit.jpg);
    background-size: cover;
  }

  .tab:nth-child(2):hover {
    transition: 0.4s ease-in-out;
  }

  .tab:nth-child(3) {
    background-image: url(../assets/images/veg.jpg);
    background-size: cover;
    transition: 0.4s ease-in-out;
  }

  .tab:nth-child(3):hover {
    // background: linear-gradient(
    //     rgba(201, 213, 109, 0.61),
    //     rgba(201, 213, 109, 0.61)
    //   ),
    //   url(../assets/images/veg.jpg);
    // background-size: cover;
    transition: 0.4s ease-in-out;
  }

  .tab:nth-child(4) {
    background-image: url(../assets/images/harvest.jpg);
    background-size: cover;
  }

  .tab:nth-child(4):hover {
    // background: linear-gradient(
    //     rgba(201, 213, 109, 0.61),
    //     rgba(201, 213, 109, 0.61)
    //   ),
    //   url(../assets/images/harvest.jpg);
    background-size: cover;
    transition: 0.4s ease-in-out;
  }

  .tab:nth-child(5) {
    background-image: url(../assets/images/calendar.jpeg);
    background-size: cover;
  }

  .tab:nth-child(5):hover {
    // background: linear-gradient(
    //     rgba(201, 213, 109, 0.61),
    //     rgba(201, 213, 109, 0.61)
    //   ),
    //   url(../assets/images/calendar.jpeg);
    background-size: cover;
    transition: 0.4s ease-in-out;
  }

  .tab:nth-child(even) {
    transform: translateX(-100%);
    opacity: 0.7;
  }

  .tab:nth-child(odd) {
    transform: translateX(100%);
    transition: 1s ease-in-out;
    opacity: 0.7;
  }

  .tab.returnPos {
    transform: translateX(0);
    opacity: 1;
  }

  .tab h1 {
    padding-bottom: 1rem;
    font-size: 2.25rem;
    color: white;
    text-shadow: 0px 0px 1px black;
    letter-spacing: 2px;
    font-weight: 500;
  }

  .tab:hover h1,
  .tab:hover p {
    transition: 0.7s;
    transform: scale(1.25);
    // transform-origin: bottom;
  }

  .tab p {
    font-family: "Montserrat", sans-serif;
    text-transform: uppercase;
    color: white;
  }
}

section#services {
  display: flex;
  -ms-flex-direction: column;
  flex-direction: column;
  min-height: 71vh;
  height: 71vh;
  background: linear-gradient(rgba(90, 80, 80, 0.45), rgba(0, 150, 136, 0.82)),
    url(../assets/images/farm.jpg);
  background-size: 100%;
  background-position: center;
  color: white;
}

section#services h1 {
  margin: 4rem;
  padding: 3rem 0rem;
}

section#services p {
  font-size: 0.9375rem;
  font-family: "Montserrat", sans-serif;
  text-align: center;
  position: absolute;
  margin: 30vh 8rem 5rem 8rem;
  line-height: 1.4rem;
}

section#ourWork a,
section#blog a:not(.more) {
  display: block;
  background-color: transparent;
  color: black;
  border: 1px solid black;
  width: 13rem;
  padding: 1rem;
  margin-top: 3rem;
  margin-left: calc(50vw - 7.5rem);
  margin-bottom: 2rem;
  text-transform: uppercase;
  cursor: pointer;
  text-decoration: none;
  font-family: helvetica, arial, sans-serif;
  font-size: 0.875rem;
  transition: 0.3s ease-in-out;
  text-align: center;
}

section#ourWork a {
  margin-left: calc(50vw - 7.5rem);
  margin-bottom: 2rem;
}

section#ourWork a:hover,
section#blog a:hover {
  color: rgba(252, 90, 93, 0.9);
  border-color: rgba(252, 90, 93, 0.9);
}

section#blog button {
  padding: 1.35rem 3.4rem;
  margin-bottom: 9rem;
}

section#services a {
  background-color: transparent;
  color: #fff;
  border: 1px solid #fff;
  width: 16rem;
  padding: 1rem;
  margin-left: calc(50vw - 8rem);
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  font-family: helvetica, arial, sans-serif;
  font-size: 0.875rem;
  text-shadow: 0px 0px 5px black;
  letter-spacing: 2px;
  text-transform: uppercase;
}

section#services a:hover {
  background-color: #ffffffa3;
  color: black;
  border: 0.1rem solid #ffc107;
  width: 16rem;
  padding: 1rem;
  margin-left: calc(50vw - 8rem);
  text-shadow: 0px 2px 5px orange;
}
section#tagLine h1 {
  padding: 6rem 2.3rem;
}
section#tagLine h1 {
  padding: 6rem 7rem;
  font-weight: 100;
  text-align: center;
  line-height: 2.5rem;
  font-family: "Playfair Display", serif;
}
section h1 {
  font-size: calc(1.75rem + 1 * ((100vw - 320px) / 680));
  margin: auto;
  padding: 6rem;
  padding-bottom: 2rem;
  font-weight: 100;
  text-align: center;
}
section h1 {
  padding: 0rem;
  padding-top: 2rem;
  padding-bottom: 2rem;
}
section#workWithUs a {
  margin-top: 6rem;
}
@media only screen and (max-width: 992px) {
  section#ourWork .tab {
    background: rgba(252, 90, 93, 0.9);
    color: #fff;
    display: inline-block;
    text-align: center;
    width: 83%;
  }
}
.tab.returnPos {
  transform: translateX(0);
  opacity: 1;
}
.anim-border {
  animation-delay: 0.4s;
  animation: 1s borderIn ease-in-out;
  animation-fill-mode: forwards;
}

@keyframes borderIn {
  0% {
    border-bottom: 3px solid transparent;
    transform: scale(0, 1);
  }
  100% {
    border-bottom: 3px solid #009688;
    transform: scale(1, 1);
  }
}
.bottom-border {
  display: block;
  max-width: 7rem;
  text-align: center;
  margin-left: calc(50% - 3.5rem);
}

.bottom-border.left {
  margin-left: 0px;
  max-width: 9rem;
  margin-bottom: 1.5rem;
}
section#services {
  display: flex;
  -ms-flex-direction: column;
  flex-direction: column;
  min-height: 71vh;
  height: 71vh;
  background: linear-gradient(rgba(90, 80, 80, 0.45), rgba(0, 150, 136, 0.82)),
    url(../assets/images/farm.jpg);
  background-size: cover;
  background-position: center;
  color: white;
}

section#services h1 {
  margin: 3rem 0 0rem;
  padding: 3rem 0rem;
}

section#services p {
  font-size: 0.9375rem;
  font-family: "Montserrat", sans-serif;
  text-align: center;
  position: relative;
  margin: 0px;
  line-height: 1.4rem;
  max-width: 90%;
  margin-left: 5%;
  margin-bottom: 2rem;
}
section#workWithUs {
  background: rgb(202, 23, 30);
  background: linear-gradient(rgba(202, 23, 30, 0.7), rgba(202, 23, 30, 1)),
    url(../assets/images/applebg.jpg);
  color: white;
  text-align: center;
  min-height: 24rem;
}
section#workWithUs a {
  background-color: transparent;
  color: #fff;
  border: 1px solid #fff;
  width: 15rem;
  padding: 1rem;
  margin-bottom: 7rem;
  cursor: pointer;
  display: block;
  text-transform: uppercase;
  text-decoration: none;
  cursor: pointer;
  font-family: helvetica, arial, sans-serif;
  font-size: 0.875rem;
  margin-left: calc(50vw - 7.5rem);
}

section#workWithUs a:hover {
  background-color: white;
  color: rgba(252, 90, 93, 1);
  color: black;
  border: 1px solid #fff;
  width: 15rem;
  padding: 1rem;
  margin-bottom: 7rem;
  outline: 1px solid rgba(252, 90, 93, 1);
  outline-offset: -4px;
}
</style>
