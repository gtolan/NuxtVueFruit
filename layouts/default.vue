<template>
  <div class="app">
    <Navbar/>
    <nuxt/>
    <Footer/>
  </div>
</template>

<script>
import Navbar from "~/components/Navbar.vue";
// import InterObserver from "~/components/intersectionObserver.js";
import Footer from "~/components/Footer.vue";
export default {
  name: "Home",
  components: {
    Navbar,
    Footer
  },
  mounted() {
    // let IO = new InterObserver();
    // console.log('IO start', IO)
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Playfair+Display&display=swap");
@import url("https://fonts.googleapis.com/css?family=Montserrat&display=swap");
/* html {
  font-family: "Monserrat", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
*/
html {
  position: relative;
  width: 100vw;
  overflow-x: hidden;
}
body {
  width: 100vw;
  margin: 0px;
  overflow-x: hidden;
}
#__nuxt,
#__layout {
  width: 100vw;
}
div.app {
  width: 100vw;
  overflow-x: hidden;
}
* {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>
