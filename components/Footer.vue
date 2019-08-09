<template>
  <footer>
    <div class="contact">
      <b>Contact</b>
      <p>Address 1.</p>
      <p>Street 2</p>
      <p>City, Country</p>
    </div>
    <div class="number">
      <p class="tel">
        <a href>+35 1 671 8806</a>
      </p>
      <p class="email">
        <a href>info@lebanesefruits.com</a>
      </p>
    </div>
    <div class="follow">
      <b>Follow Us</b>

      <a href>Facebook</a>
      <a href>Twitter</a>
      <a href>Linkedin</a>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer"
};
</script>

<style lang="scss" scoped>
footer {
  min-height: 10rem;
  background-color: white;
  display: grid;
  grid-template-columns: 3fr 6fr 5fr;
  padding: 5rem 6rem 0rem 6rem;
  font-family: "Montserrat", sans-serif;
  font-size: 0.8rem;
}

footer a {
  color: rgba(252, 90, 93, 1);
  text-decoration: none;
  font-weight: 200;
}

footer .contact p {
  line-height: 1rem;
  font-weight: 100;
  margin: 0.3rem 0rem;
}

/*footer .social-med {*/
/*display: grid;*/
/*grid-template-columns: 1fr 1fr 1fr 1fr;*/
/*}*/

footer .follow {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1rem 1fr;
  text-align: left;
}

footer .follow > b {
  grid-column-start: 1;
  grid-column-end: 5;
}

.follow a:nth-child(2) {
  grid-column-start: 1;
  grid-column-end: 2;
  grid-row-start: 2;
}

.follow a:nth-child(3) {
  grid-column-start: 2;
  grid-column-end: 3;
  grid-row-start: 2;
}

.follow a:nth-child(4) {
  grid-column-start: 3;
  grid-column-end: 4;
  grid-row-start: 2;
}

.follow a:nth-child(5) {
  grid-column-start: 4;
  grid-column-end: 5;
  grid-row-start: 2;
}

.tel:before {
  content: "T |";
}

.email:before {
  content: "E |";
}
@media only screen and (max-width: 992px) {
  footer {
    padding: 23px;
    padding-top: 2rem;
    display: grid;
    grid-template-columns: 6fr 6fr;
  }
}
</style>