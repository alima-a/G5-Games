<template>
  <div id="app">
    <app-header />
    <main>
      <app-slider :pictures="pictures" />
    </main>
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader";
import AppSlider from "@/components/AppSlider";
import { getCookie, setCookie } from "@/helpers/cookiesHelper";

const COOKIE_EXP_TIME = 1000 * 60 * 5;

export default {
  name: "App",
  components: {
    AppSlider,
    AppHeader,
  },
  data() {
    return {
      pictures: [],
      isPicturesLoaded: false,
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
      fetch("https://random.dog/woof.json")
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
  },
  beforeMount() {
    this.getPictures();
  },
};
</script>
<style lang="scss">
* {
  font-family: "Inter", sans-serif;
  font-size: 16px;
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
