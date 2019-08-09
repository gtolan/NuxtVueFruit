<template>
  <div>
    <h1>
      Latest News
      <span class="bottom-border" ref="borderBottom"></span>
    </h1>
    <section class="news">
      <article class="card" v-for="card in cards" :key="card.id">
        <img :src="card.img">
        <h4 class="title">{{card.title}}</h4>
        <p class="author">By {{card.author}}</p>
        <p class="date">{{card.date}}</p>
        <p class="text">{{card.text}}</p>
      </article>
      <a href class="read-more">Read More</a>
    </section>
  </div>
</template>

<script>
export default {
  name: "NewsSection",
  components: {},
  data() {
    return {
      observer: null,
      options: {
        root: null,
        rootMargin: "0px",
        // threshold: .5
        threshold: this.buildThresholdList()
      },
      cards: [
        {
          img: require("../assets/images/harvest2.jpg"),
          id: 1,
          title: "Title 1",
          text: "text...",
          date: "date",
          author: "brahim"
        },
        {
          img: require("../assets/images/safety.jpg"),
          id: 1,
          title: "Title 2",
          text: "text...",
          date: "date",
          author: "Hossam"
        },
        {
          img: require("../assets/images/package.jpg"),
          id: 1,
          title: "Title 3",
          text: "text...",
          date: "date",
          author: "Abood"
        },
        {
          img: require("../assets/images/harvest.jpg"),
          id: 4,
          title: "Title 4",
          text: "text...",
          date: "date",
          author: "Abood"
        }
      ]
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
      });
    }
  },
  mounted() {
    this.observer = new IntersectionObserver(
      this.handleIntersect,
      this.options
    );
    let el = this.$refs.borderBottom;
    this.observer.observe(el);
  }
};
</script>

<style lang="scss" scoped>
section.news {
  display: flex;
  flex-wrap: wrap;
  justify-content: left;
  article {
    width: 45vw;
    margin: 2.5vw;
    padding: 10px;
    box-shadow: -3px 5px 10px 3px #808080b0;
    img {
      width: 100%;
      min-height: 300px;
      max-height: 300px;
    }
    h4.title {
      font-size: 2rem;
    }
  }
}
@media only screen and (max-width: 762px) {
  section.news article {
    width: 90vw;
    margin: 5vw;
  }
}
@media only screen and (min-width: 1024px) {
  section.news article {
    width: 27vw;
    margin: 3.15vw;
  }
}

h1 {
  padding: 0rem;
  padding-top: 6rem;
  font-size: calc(1.75rem + 1 * ((100vw - 320px) / 680));
  margin: auto;
  font-weight: 100;
  text-align: center;
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
a.read-more {
  display: block;
  background-color: transparent;
  color: #000;
  border: 1px solid #000;
  width: 15rem;
  padding: 1rem;
  margin-top: 3rem;
  margin-left: calc(50vw - 7.5rem);
  margin-right: calc(50vw - 7.5rem);
  margin-bottom: 2rem;
  text-transform: uppercase;
  cursor: pointer;
  text-decoration: none;
  font-family: helvetica, arial, sans-serif;
  font-size: 0.875rem;
  -webkit-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
  text-align: center;
  &:hover {
    color: white;
    border-color: rgba(252, 90, 93, 0.9);
    background-color: black;
    outline: 1px solid rgba(252, 90, 93, 1);
    outline-offset: -4px;
  }
}
</style>