<template>
  <app-container>
    <div ref="swiper" class="slider swiper">
      <div :key="slidesPerView" class="swiper-wrapper">
        <div v-for="picture in pictures" :key="picture" class="swiper-slide">
          <img class="slider__img" :src="picture" alt="" />
        </div>
      </div>
      <div class="swiper-pagination"></div>
      <div class="swiper-button-prev">
        <img
          class="slider__arrow slider__arrow_prev"
          src="../assets/images/arrow.png"
          alt="arrow"
        />
      </div>
      <div class="swiper-button-next">
        <img
          class="slider__arrow slider__arrow_next"
          src="../assets/images/arrow.png"
          alt="arrow"
        />
      </div>
      <div class="swiper-scrollbar"></div>
    </div>
  </app-container>
</template>

<script>
import AppContainer from "@/components/AppContainer";
import Swiper, { Navigation, Pagination } from "swiper";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

export default {
  name: "AppSlider",
  components: { AppContainer },
  props: {
    pictures: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      slidesPerView: 3,
    };
  },
  methods: {
    handleResize() {
      this.slidesPerView = window.innerWidth > 834 ? 3 : 1;
    },
    initSwiper() {
      new Swiper(this.$refs.swiper, {
        modules: [Navigation, Pagination],
        loop: true,
        pagination: {
          el: ".swiper-pagination",
        },
        spaceBetween: 30,
        slidesPerView: this.slidesPerView,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        scrollbar: {
          el: ".swiper-scrollbar",
        },
      });
    },
  },
  created() {
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener("resize", this.handleResize);
  },
  mounted() {
    this.initSwiper();
  },
  updated() {
    // Reinitializes the swiper if the number of slides has changed
    // This is necessary in order to make it more convenient to test
    // the slider by manually resizing the browser window.
    this.initSwiper();
  },
};
</script>

<style scoped lang="scss">
.slider {
  padding-top: 16px;
  height: 338px;
  @media (max-width: 1920px) {
    height: 308px;
  }
  @media (max-width: 1440px) {
    height: 286px;
  }
  @media (max-width: 1280px) {
    height: 222px;
  }
  @media (max-width: 1024px) {
    height: 202px;
  }
  @media (max-width: 834px) {
    height: 244px;
  }
  @media (max-width: 744px) {
    padding-top: 8px;
    height: 154px;
  }
  @media (max-width: 430px) {
    height: 170px;
  }
  @media (max-width: 375px) {
    height: 164px;
  }
  &__img {
    width: 442px;
    height: 294px;
    object-fit: cover;
    @media (max-width: 1920px) {
      width: 410px;
      height: 272px;
    }
    @media (max-width: 1440px) {
      width: 378px;
      height: 250px;
    }
    @media (max-width: 1280px) {
      width: 282px;
      height: 187px;
    }
    @media (max-width: 1024px) {
      width: 252px;
      height: 167px;
    }
    @media (max-width: 834px) {
      width: 658px;
      height: 208px;
    }
    @media (max-width: 744px) {
      width: 412px;
      height: 130px;
    }
    @media (max-width: 430px) {
      width: 324px;
      height: 143px;
    }
    @media (max-width: 375px) {
      width: 276px;
      height: 143px;
    }
  }
  &__arrow {
    height: 48px;
    width: 48px;
    &_prev {
      transform: rotate(180deg);
    }
    @media (max-width: 1920px) {
      height: 40px;
      width: 40px;
    }
    @media (max-width: 1280px) {
      width: 32px;
      height: 32px;
    }
    @media (max-width: 744px) {
      width: 24px;
      height: 24px;
    }
    &:hover {
      opacity: 0.9;
    }
  }
}
.swiper-pagination {
  bottom: -4px;
}
::v-deep(.swiper-pagination-bullet) {
  height: 12px;
  width: 12px;
  @media (max-width: 744px) {
    height: 8px;
    width: 8px;
  }
}
::v-deep(.swiper-pagination-bullet-active) {
  background: $second-background-color;
}
.swiper-button-next,
.swiper-button-prev {
  &:after {
    display: none;
  }
}

.swiper-button-prev {
  left: 21px;
  @media (max-width: 1920px) {
    left: 15px;
  }
  @media (max-width: 1280px) {
    left: 11px;
  }
  @media (max-width: 744px) {
    left: 6px;
  }
  @media (max-width: 430px) {
    left: 8px;
  }
  @media (max-width: 375px) {
    left: 3px;
  }
}
.swiper-button-next {
  right: 21px;
  @media (max-width: 1920px) {
    right: 15px;
  }
  @media (max-width: 1280px) {
    right: 11px;
  }
  @media (max-width: 744px) {
    right: 6px;
  }
  @media (max-width: 430px) {
    right: 8px;
  }
  @media (max-width: 375px) {
    right: 3px;
  }
}
</style>
