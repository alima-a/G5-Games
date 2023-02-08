<template>
  <div id="app">
    <app-header @fetchProducts="fetchProducts" />
    <main>
      <app-slider :pictures="pictures" />
      <app-cards-block :products="products" />
    </main>
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader";
import AppSlider from "@/components/AppSlider";
import { getCookie, setCookie } from "@/helpers/cookiesHelper";
import { GET_PICTURE_URL, GET_PRODUCTS_URL } from "@/api";
import AppCardsBlock from "@/components/AppCardsBlock";

const COOKIE_EXP_TIME = 1000 * 60 * 5;

export default {
  name: "App",
  components: {
    AppCardsBlock,
    AppSlider,
    AppHeader,
  },
  data() {
    return {
      pictures: [],
      isPicturesLoaded: false,
      products: [],
    };
  },
  watch: {
    isPicturesLoaded(value) {
      if (value) {
        const cookieValue = this.pictures.join(",");
        setCookie("g5-pictures", cookieValue, COOKIE_EXP_TIME);
      }
    },
  },
  methods: {
    isImageCheck(url) {
      return /\.(jpg|jpeg|png|webp|avif|svg|PNG|JPG)$/.test(url);
    },
    fetchPictures() {
      fetch(GET_PICTURE_URL)
        .then((response) => response.json())
        .then((data) => {
          if (this.isImageCheck(data.url)) {
            this.pictures.push(data.url);
          }
          if (this.pictures.length < 10) {
            this.fetchPictures();
          } else {
            this.isPicturesLoaded = true;
          }
        });
    },
    getPictures() {
      const cookieValue = getCookie("g5-pictures");
      if (cookieValue) {
        this.pictures = cookieValue.split(",");
      } else {
        this.fetchPictures();
      }
    },
    fetchProducts() {
      fetch(GET_PRODUCTS_URL)
        .then((response) => response.json())
        .then((data) => {
          // I'm not sure I understood the conditions for the update button correctly,
          // but the commented out option will add 100 products each time.
          // And the current version just updates the list of products
          // this.products = this.products.concat(data.products);
          this.products = data.products;
          localStorage.setItem("products", JSON.stringify(this.products));
        });
    },
    getProducts() {
      const products = localStorage.getItem("products");
      if (products) {
        this.products = this.products.concat(JSON.parse(products));
      } else {
        this.fetchProducts();
      }
    },
  },
  beforeMount() {
    this.getPictures();
    this.getProducts();
  },
};
</script>
<style lang="scss">
* {
  font-family: "Inter", sans-serif;
  color: $main-font-color;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
}
main {
  width: 100%;
  height: 100%;
  background-color: $main-background-color;
}
</style>
