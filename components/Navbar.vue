<template>
  <div>
    <div ref="navWatch" id="navWatch"></div>
    <nav ref="navbar">
      <button class="hamburger hamburger--vortex" type="button">
        <span class="hamburger-box">
          <span class="hamburger-inner"></span>
        </span>
      </button>

      <ul class="options left desktop">
        <li class="drop">
          <a href="about">About</a>
          <ul class="dropdown-group">
            <li class="drop-item">
              <a href="/our-company">Our Company</a>
            </li>
            <li class="drop-item">
              <a href="/our-team">Our Team</a>
            </li>
            <li class="drop-item">
              <a href="/retailers">Retailers</a>
            </li>
          </ul>
        </li>
        <li class="drop">
          <a href="products">Products</a>
          <ul class="dropdown-group">
            <li class="drop-item">
              <a href="/products/fruit">Fruit</a>
            </li>
            <li class="drop-item">
              <a href="/products/vegetables">Vegetables</a>
            </li>
          </ul>
        </li>
      </ul>
      <a
        href="/home"
        class="logo"
        title="Lebanese Fruit Home"
        aria-label="Lebanese Fruit Home"
        id="logo"
      >
        <img src="../assets/lebfruit.jpg">
      </a>
      <div class="options right desktop">
        <div class="dropdown">
          <a href="/news" class="dropbtn">
            News
            <i class="fa fa-caret-down"></i>
          </a>
        </div>
        <div class="dropdown">
          <a href="/contact" class="dropbtn">
            Contact
            <i class="fa fa-caret-down"></i>
          </a>
        </div>
      </div>
    </nav>
  </div>
</template>
  <script>
// import EventBus from "../eventBus";
export default {
  name: "Navbar",
  data() {
    return {
      slate: false,
      cartItems: [],
      observer: null,
      options: {
        root: null,
        rootMargin: "0px",
        // threshold: .5
        threshold: this.buildThresholdList()
      }
    };
  },
  props: ["cart", "totalQty"],
  filters: {
    itemAmount: val => {
      return val == 1 ? val + " Item" : val + " Items";
    }
  },
  mounted() {
    this.changeNav();
    this.startNavObserver();
    // EventBus.$on("addToCart", value => {
    //   this.addToCart(value);
    // });
    // EventBus.$on("deleteItem", value => {
    //   this.deleteItem(value);
    // });
  },
  updated() {
    this.changeNav();
  },
  watch: {
    // call again the method if the route changes
    $route: "changeNav"
  },
  methods: {
    buildThresholdList() {
      let thresholds = [];
      let numSteps = 20;

      for (let i = 1.0; i <= numSteps; i++) {
        let ratio = i / numSteps;
        thresholds.push(ratio);
      }

      thresholds.push(0);
      return thresholds;
    },
    startNavObserver() {
      this.observer = new IntersectionObserver(
        this.handleIntersect,
        this.options
      );
      this.observer.observe(this.$refs.navWatch);
      console.log("watching nav watch");
    },
    handleIntersect(entries, observer) {
      this.observer = observer;

      entries.forEach(entry => {
        console.log(entry.target.id);
        if (entry.intersectionRatio < 0.6 && entry.target.id == "navWatch") {
          this.$refs.navbar.classList.add("fixed-nav");
        } else if (
          entry.intersectionRatio > 0.6 &&
          entry.target.id == "navWatch"
        ) {
          this.$refs.navbar.classList.remove("fixed-nav");
        }
      });
    },
    changeNav() {
      if (
        this.$route.path.startsWith("/products") ||
        this.$route.path.startsWith("/cart") ||
        this.$route.path.startsWith("/all") ||
        this.$route.path.startsWith("/mens") ||
        this.$route.path.startsWith("/womens")
      ) {
        this.slate = true;
      } else {
        this.slate = false;
      }
    },
    addToCart(itemToAdd) {
      let inBasket = false;
      this.cartItems.forEach(item => {
        if (item.id === itemToAdd.id) {
          inBasket = true;
          item.qty += itemToAdd.qty;
        }
      });
      if (inBasket === false) {
        this.cartItems.push(itemToAdd);
      }
      itemToAdd.qty = 1;
    },
    deleteItem(itemToDelete) {
      function removeItem(val) {
        return val.id !== itemToDelete.id;
      }
      var removed = this.cartItems.filter(removeItem);
      this.cartItems = removed;
    }
  }
};
</script>

<style lang="scss" >
nav {
  display: grid;
  grid-template-columns: 3fr 2fr 3fr;
  animation: slideDownInit 1.4s ease-in;
  animation-fill-mode: forwards !important;
  transform: translateY(-200px);
  background-color: white;
  will-change: transform, opacity;
  text-align: center;
  z-index: 3;
  position: relative;
  width: 100vw;

  .options.right-desktop {
    display: none;
  }

  a.logo {
    height: 4rem;
    display: inline-block;
    text-decoration: none;
    color: white;
    transition: 1.5s ease-in-out;

    img {
      height: 11rem;
    }
  }
}

nav div.options.right.desktop {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  grid-template-columns: 1fr 1fr;

  div.dropdown {
    text-align: center;

    a.dropbtn {
      width: 100%;
      padding: 4.5rem 1rem 3.5rem;
      position: relative;
      font-family: Montserrat, sans-serif;
      font-size: 1.275rem;
      border: 0;
      outline: 0;
      color: #000;
      background-color: transparent;
      font-weight: 100;
      text-transform: uppercase;
      -webkit-transition: 0.2s ease-in;
      transition: 0.2s ease-in;
      text-decoration: none;
    }

    &:hover {
      cursor: pointer;

      a.dropbtn {
        color: red;
      }
    }
  }
}
nav.fixed-nav div.options.right.desktop div.dropdown a.dropbtn {
  padding: 1.5rem 1rem 1.5rem;
}

@media only screen and (min-width: 992px) {
  nav {
    box-shadow: 0px 0px 3px;

    .options.right.desktop {
      font-weight: 100;
      //display: flex;
      ul {
        display: none;
      }

      a {
        text-transform: uppercase;
        font-size: 1.25rem;
        font-size: 0.875rem;
        letter-spacing: 1px;
        color: white;
        text-decoration: none;
        //padding: 4.5rem 1rem;
        font-family: "Montserrat", sans-serif;
        text-align: center;
        float: right;

        &:hover + ul {
          display: block;
          top: 4rem;
          padding-left: 9px;
          list-style: none;
          background-color: green;
        }

        &:nth-child(1):hover + ul {
          grid-column-start: 1;
          grid-column-end: 3;
          grid-row-start: 2;
          margin: 0px;
          padding-left: 3px;
        }

        a ul li {
          padding: 1rem 0rem;
        }
      }
    }

    button.hamburger {
      display: none;
    }

    &.fixed-nav {
      ul.options.left.desktop li.drop a {
        padding: 1.5rem 1rem;
      }

      ul.options.left.desktop li.drop ul.dropdown-group {
        position: absolute;
        top: 4rem;
      }

      div.dropdown {
        text-align: center;

        a.dropbtn {
          width: 100%;
          padding: 1.5rem 1rem 1.5rem;
        }
      }
    }
  }

  a.dropbtn {
    display: inline-block;
    color: #000;
    text-decoration: none;
    padding: 4.5rem 1rem 3.5rem;
    background-color: transparent;
    border: none;
    font-family: Montserrat, sans-serif;
    font-size: 1.275rem;
    text-transform: uppercase;
    font-family: Montserrat, sans-serif;
    font-weight: 100;
  }

  .navbar a:hover,
  .dropdown:hover .dropbtn {
    color: red;
  }
  nav.fixed-nav .options.right-desktop {
    height: 1rem;
  }
}

nav.fixed-nav {
  background-color: white;
  position: fixed;
  top: 0px;
  width: 100vw;
  height: 4rem;
  transition: ease-in-out;
  z-index: 10;
}
nav.fixed-nav {
  background-color: #ffffffe3;
  position: fixed;
  top: 0px;
  width: 100vw;
  height: 4rem;
  transition: ease-in-out;
  z-index: 10;
}
nav.fixed-nav .options.right-desktop a,
nav.fixed-nav .options.right-desktop .dropdown .dropbtn {
  color: black;
  padding: 0.8rem 1rem;
}

nav.fixed-nav a.logo {
  color: black;
  padding-top: 0.1rem;
  transform: scale(0.5);
  transform-origin: top;
}
nav.fixed-nav {
  a.dropbtn {
    display: inline-block;
    color: #000;
    text-decoration: none;
    padding: 1.5rem 1rem 1.5rem;
  }
}
nav .options.right-desktop .dropdown .dropdown-content a:hover {
  background-color: #444141;
  color: #fc5a5d;
}

@media only screen and (max-width: 992px) {
  header nav .options.right-desktop {
    display: none;
  }
}

.dropdown:hover button.dropbtn {
  background-color: white;
}

@keyframes slideDownInit {
  0% {
    opacity: 0;
    transform: translateY(-200px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
}

//@media only screen and (max-width: 992px)

@media only screen and (max-width: 992px) {
  nav .options.right.desktop,
  nav .options.left.desktop {
    display: none !important;
  }
}
//@media only screen and (max-width: 992px)

//@media only screen and (min-width: 992px)
@media only screen and (min-width: 992px) {
  nav {
    .options.right.desktop {
      font-weight: 100;
      //display: flex;
      ul {
        display: none;
      }

      a {
        text-transform: uppercase;
        font-size: 1.25rem;
        font-size: 0.875rem;
        letter-spacing: 1px;
        color: white;
        text-decoration: none;
        //padding: 4.5rem 1rem;
        font-family: "Montserrat", sans-serif;
        text-align: center;
        float: right;

        &:hover + ul {
          display: block;
          top: 4rem;
          padding-left: 9px;
          list-style: none;
          background-color: green;
        }

        &:nth-child(1):hover + ul {
          grid-column-start: 1;
          grid-column-end: 3;
          grid-row-start: 2;
          margin: 0px;
          padding-left: 3px;
        }

        a ul li {
          padding: 1rem 0rem;
        }
      }
    }

    button.hamburger {
      display: none;
    }

    &.fixed-nav {
      ul.options.left.desktop li.drop a {
        padding: 1.5rem 1rem;
      }

      ul.options.left.desktop li.drop ul.dropdown-group {
        position: absolute;
        top: 4rem;
      }

      div.dropdown {
        text-align: center;

        a.dropbtn {
          width: 100%;
          padding: 1.5rem 1rem 1.5rem;
        }
      }
    }
  }

  a.dropbtn {
    display: inline-block;
    color: #000;
    text-decoration: none;
    padding: 4.5rem 1rem 3.5rem;
    background-color: transparent;
    border: none;
    font-family: Montserrat, sans-serif;
    font-size: 1.275rem;
    text-transform: uppercase;
    font-family: Montserrat, sans-serif;
    font-weight: 100;
  }

  .navbar a:hover,
  .dropdown:hover .dropbtn {
    color: red;
  }

  nav .options.right-desktop .dropdown .dropdown-content a:hover {
    background-color: #444141;
    color: #fc5a5d;
  }
}

ul.options.left.desktop {
  margin: 0px;
  padding: 0rem;
  list-style: none;
  display: grid;
  grid-template-columns: 1fr 1fr;

  li.drop {
    position: relative;
    font-family: Montserrat, sans-serif;
    font-size: 1.275rem;
    border: 0;
    outline: 0;
    color: #000;
    background-color: transparent;
    font-weight: 100;
    text-transform: uppercase;
    -webkit-transition: 0.2s ease-in;
    transition: 0.2s ease-in;
    text-decoration: none;

    a {
      position: relative;
      display: inline-block;
      color: black;
      text-decoration: none;
      padding: 4.5rem 1rem 3.5rem;

      &:hover {
        color: red;
      }
    }

    &:hover > ul.dropdown-group {
      visibility: visible;
      opacity: 1;
      display: block;
      transform-origin: top;
      animation-fill-mode: forwards;
      animation: 0.5s scaleDownOpen;
    }

    ul.dropdown-group {
      position: absolute;
      top: 9.5rem;
      box-shadow: 0px 5px 2px 2px #736d6dba;
      margin-left: 6rem;
      text-align: left;
      background-color: #fff;
      display: none;
      margin: 0;
      width: 98%;
      padding: 0;
      overflow: hidden;
      margin-left: 0.1rem;

      li.drop-item {
        padding: 0.5rem 1rem;
        clear: both;
        width: 100%;
        position: relative;

        &:hover {
          background-color: #efeaea;

          a {
            color: red;
          }
        }

        a {
          padding: 0px;
          position: relative;
        }
      }
    }
  }
}

a.arrow-down {
  margin-top: 11rem;
}
nav a.logo img {
  height: 11rem;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  -webkit-box-shadow: 0 0 3px 2px #d3d3d3;
  box-shadow: 0 0 3px 2px #d3d3d3;
}
// Hamburger
// ==================================================
$hamburger-padding-x: 15px !default;
$hamburger-padding-y: 15px !default;
$hamburger-layer-width: 40px !default;
$hamburger-layer-height: 4px !default;
$hamburger-layer-spacing: 6px !default;
$hamburger-layer-color: #591719 !default;
$hamburger-layer-border-radius: 4px !default;
$hamburger-hover-opacity: 0.7 !default;
$hamburger-active-layer-color: $hamburger-layer-color !default;
$hamburger-active-hover-opacity: $hamburger-hover-opacity !default;
$hamburger-hover-use-filter: false !default;
$hamburger-hover-filter: opacity(50%) !default;
$hamburger-active-hover-filter: $hamburger-hover-filter !default;

$hamburger-types: (collapse) !default;

.hamburger--vortex {
  .hamburger-inner {
    transition-duration: 0.2s;
    transition-timing-function: cubic-bezier(0.19, 1, 0.22, 1);

    &::before,
    &::after {
      transition-duration: 0s;
      transition-delay: 0.1s;
      transition-timing-function: linear;
    }

    &::before {
      transition-property: top, opacity;
    }

    &::after {
      transition-property: bottom, transform;
    }
  }

  &.is-active {
    .hamburger-inner {
      transform: rotate(765deg);
      transition-timing-function: cubic-bezier(0.19, 1, 0.22, 1);

      &::before,
      &::after {
        transition-delay: 0s;
      }

      &::before {
        top: 0;
        opacity: 0;
      }

      &::after {
        bottom: 0;
        transform: rotate(90deg);
      }
    }
  }
}

.hamburger {
  padding: $hamburger-padding-y $hamburger-padding-x;
  display: inline-block;
  cursor: pointer;
  width: 5rem;
  margin-left: 0.3rem;
  transition-property: opacity, filter;
  transition-duration: 0.15s;
  transition-timing-function: linear;
  border: 1px solid lightgrey;
  border-radius: 4px;
  transform: scale(0.9);
  // Normalize (<button>)
  font: inherit;
  color: inherit;
  text-transform: none;
  background-color: transparent;
  border: 0;
  margin: 0;
  overflow: visible;

  &:hover {
    @if $hamburger-hover-use-filter == true {
      filter: $hamburger-hover-filter;
    } @else {
      opacity: $hamburger-hover-opacity;
    }
  }

  &.is-active {
    &:hover {
      @if $hamburger-hover-use-filter == true {
        filter: $hamburger-active-hover-filter;
      } @else {
        opacity: $hamburger-active-hover-opacity;
      }
    }

    .hamburger-inner,
    .hamburger-inner::before,
    .hamburger-inner::after {
      background-color: $hamburger-active-layer-color;
    }
  }
}

.hamburger-box {
  margin-top: -4px;
  margin-left: -3px;
  width: $hamburger-layer-width;
  height: $hamburger-layer-height * 3 + $hamburger-layer-spacing * 2;
  display: inline-block;
  position: relative;
}

.hamburger-inner {
  display: block;
  top: 50%;
  margin-top: $hamburger-layer-height / -2;

  &,
  &::before,
  &::after {
    width: $hamburger-layer-width;
    height: $hamburger-layer-height;
    background-color: $hamburger-layer-color;
    border-radius: $hamburger-layer-border-radius;
    position: absolute;
    transition-property: transform;
    transition-duration: 0.15s;
    transition-timing-function: ease;
  }

  &::before,
  &::after {
    content: "";
    display: block;
  }

  &::before {
    top: ($hamburger-layer-spacing + $hamburger-layer-height) * -1;
  }

  &::after {
    bottom: ($hamburger-layer-spacing + $hamburger-layer-height) * -1;
  }
}

@if index($hamburger-types, collapse) {
  /*
     * Collapse
     */
  .hamburger--collapse {
    .hamburger-inner {
      top: auto;
      bottom: 0;
      transition-duration: 0.13s;
      transition-delay: 0.13s;
      transition-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);

      &::after {
        top: ($hamburger-layer-spacing * 2 + $hamburger-layer-height * 2) * -1;
        transition: top 0.2s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
          opacity 0.1s linear;
      }

      &::before {
        transition: top 0.12s 0.2s cubic-bezier(0.33333, 0.66667, 0.66667, 1),
          transform 0.13s cubic-bezier(0.55, 0.055, 0.675, 0.19);
      }
    }

    &.is-active {
      .hamburger-inner {
        transform: translate3d(
            0,
            ($hamburger-layer-spacing + $hamburger-layer-height) * -1,
            0
          )
          rotate(-45deg);
        transition-delay: 0.22s;
        transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);

        &::after {
          top: 0;
          opacity: 0;
          transition: top 0.2s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
            opacity 0.1s 0.22s linear;
        }

        &::before {
          top: 0;
          transform: rotate(-90deg);
          transition: top 0.1s 0.16s cubic-bezier(0.33333, 0, 0.66667, 0.33333),
            transform 0.13s 0.25s cubic-bezier(0.215, 0.61, 0.355, 1);
        }
      }
    }
  }
}
@keyframes scaleDownOpen {
  0% {
    transform: scale(1, 0);
  }
  100% {
    transform: scale(1, 1);
  }
}
</style>