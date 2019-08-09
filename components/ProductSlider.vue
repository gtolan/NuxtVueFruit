<template>
  <div>
    <div class="button-group">
      <button class="active">Lebanese Harvest</button>
      <button>South African Harvest</button>
      <button>Australian Harvest</button>
    </div>
    <div class="product-slider">
      <img src="../assets/images/products/fruits/apple-product.jpeg">
      <img src="../assets/images/products/fruits/pear-product.png">
      <img src="../assets/images/products/fruits/orange-product.png">
      <img src="../assets/images/products/fruits/banana-product.jpg">
      <img src="../assets/images/products/fruits/mango-product.jpeg">
      <img src="../assets/images/products/fruits/straw-product.png">
      <img src="../assets/images/products/fruits/kiwi-product.jpg">
    </div>
    <div class="button-group toggle">
      <button class="active">Fruits</button>
      <button>Vegetables</button>
    </div>

    <a class="products-link" href="/products">All Products</a>
  </div>
</template>

<script>
export default {
  name: "ProductSlider"
};
</script>

<style lang="scss" scoped>
.button-group {
  width: 80%;
  margin: auto;
  margin-top: 5rem;
  text-align: center;

  span {
    display: inline-block;
    width: 3rem;
    height: 3rem;
    overflow: hidden;
    border-radius: 50%;
    vertical-align: middle;
    margin-right: 0.5rem;

    img.flag {
      width: 100%;
      height: 100%;
    }
  }
}

.button-group button {
  border-radius: 29px;
  border: 1px #228b22 solid;
  background-color: #fff;
  padding: 1rem;
  font-size: 0.9rem;
  color: #228b22;
  margin: 10px;
  cursor: pointer;
}

.button-group.toggle {
  margin-top: 3rem;
}

.button-group.toggle button {
  border-radius: 29px;
  border: 1px #228b22 solid;
  background-color: #fff;
  padding: 1rem;
  font-size: 0.9rem;
  cursor: pointer;
  color: #228b22;
  margin: 0px;
  min-width: 7rem;
}

.button-group.toggle button:nth-child(1) {
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;
}

.button-group.toggle button:nth-child(2) {
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
}

.product-slider {
  display: flex;
  max-width: 76%;
  overflow-x: scroll;
  overflow-y: hidden;
  margin: auto;
  border: 1px solid lightgrey;
  border-radius: 10px;
  margin-top: 1rem;
  background-color: white;
  transition: 0.4s ease-in-out;

  &.enlarge {
    display: inline-block;
    margin-left: 2%;

    &:before {
      display: none;
    }

    &:after {
      display: none;
    }
  }
}

a.products-link,
section#blog a:not(.more) {
  display: block;
  background-color: transparent;
  color: black;
  border: 1px solid black;
  width: 15rem;
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

a.products-link {
  margin-left: calc(50vw - 7.5rem);
  margin-bottom: 2rem;
}

a.products-link:hover,
section#blog a:hover {
  color: rgba(252, 90, 93, 0.9);
  border-color: rgba(252, 90, 93, 0.9);
}

.product-slider:hover:before {
  padding: 1rem;
  content: "\005E";
  margin-left: -5%;
  margin-top: 2rem;
  position: absolute;
  font-size: 5rem;
  transform: rotate(270deg);
  color: #9e9e9e;
}

.product-slider:hover:after {
  padding: 1rem;
  content: "\005E";
  margin-left: 80%;
  margin-top: 2rem;
  position: absolute;
  font-size: 5rem;
  transform: rotate(90deg);
  color: #9e9e9e;
}

.button-group button.active,
.button-group button:hover {
  border: 1px #228b22 solid;
  background-color: #6ca927;
  background: linear-gradient(
    90deg,
    rgba(54, 181, 10, 1) 0%,
    rgba(25, 121, 9, 1) 100%,
    rgba(0, 212, 255, 1) 100%
  );
  color: white;
}

.button-group button:hover {
  background-color: #8bc34a;
}

.product-slider img {
  min-width: 9.5rem;
  height: 10rem;
  padding: 1rem;
  overflow: hidden;
  transition: 0.3s ease-in-out;
  cursor: pointer;
  max-width: 9.5rem;
}

.product-slider img:hover {
  transform: scale(1.13, 1.13);
  transform-origin: center;
}
@media only screen and (min-width: 580px) and (max-width: 992px) {
  section#services a {
    margin-top: 3rem;
  }
  .product-slider:hover:after,
  .product-slider:hover:before {
    display: none;
  }
  section#services {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-direction: column;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    flex-direction: column;
    min-height: 60vh;
    height: 61vh;
  }
}
@media only screen and (max-width: 992px) {
  .button-group {
    width: 95%;
  }
  .button-group button {
    margin: 0px 0px;
    margin-bottom: 7px;
  }
  .product-slider {
    max-width: 90%;
  }
  .product-slider img {
    min-width: 7rem;
    height: 8rem;
    padding: 1rem;
    overflow: hidden;
    -webkit-transition: 0.3s ease-in-out;
    transition: 0.3s ease-in-out;
    cursor: pointer;
    max-width: 5.5rem;
  }
}
</style>