<template>
  <div class="card">
    <div
      class="card__thumbnail"
      :style="`background-image: url(${product.thumbnail})`"
    >
      <div v-if="index === 0" class="card__label card__label_top">TOP</div>
      <div v-if="index === 1" class="card__label card__label_sale">SALE</div>
      <div v-if="index === 2" class="card__label card__label_popular">
        POPULAR
      </div>
    </div>
    <p class="card__text">
      <span>Brand:</span>
      {{ product.brand }}
    </p>
    <p class="card__text">
      <span>Category:</span>
      {{ product.category | capitalizeFirstLetter }}
    </p>
    <p class="card__text card__text_desc">
      <span>Description:</span>
      {{ product.description }}
    </p>
    <p class="card__text">
      <span>Stock:</span>
      {{ count }}
    </p>
  </div>
</template>

<script>
import { getRandomNumber } from "@/helpers/mathHelpers";

export default {
  name: "AppCard",
  props: {
    product: {
      type: Object,
      default: () => {},
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      count: 0,
      interval: null,
    };
  },
  watch: {
    count(value) {
      if (value === 0) {
        clearInterval(this.interval);
      }
    },
  },
  filters: {
    capitalizeFirstLetter(value) {
      if (!value) return "";
      value = value.toString();
      return value[0].toUpperCase() + value.slice(1);
    },
  },
  methods: {
    initProductStockCounter() {
      this.count = this.product.stock;
      if (this.count) {
        const intervalTime = getRandomNumber(4) * 1000;
        this.interval = setInterval(() => {
          if (this.count > 0) {
            this.count--;
          }
        }, intervalTime);
      }
    },
  },
  beforeMount() {
    this.initProductStockCounter();
  },
};
</script>

<style scoped lang="scss">
.card {
  border: 1px solid $border-color;
  padding: 9px;
  margin-bottom: 24px;
  width: 324px;
  height: 378px;
  @media (max-width: 1920px) {
    padding: 8px;
    width: 300px;
    height: 350px;
  }
  @media (max-width: 1440px) {
    width: 276px;
    height: 322px;
    margin-bottom: 16px;
  }
  @media (max-width: 1280px) {
    width: 282px;
    height: 329px;
    padding: 7px;
  }
  @media (max-width: 1024px) {
    width: 252px;
    height: 294px;
    padding: 6px;
  }
  @media (max-width: 834px) {
    width: 314px;
    height: 366px;
    padding: 7px;
  }
  @media (max-width: 744px) {
    width: 412px;
    height: 412px;
    padding: 9px;
    margin-bottom: 8px;
  }
  @media (max-width: 430px) {
    width: 324px;
    height: 324px;
    padding: 7px;
  }
  @media (max-width: 375px) {
    width: 276px;
    height: 276px;
    padding: 6px;
  }
  &__thumbnail {
    position: relative;
    width: 306px;
    height: 206px;
    background-position: top left;
    background-size: cover;
    background-repeat: no-repeat;
    @media (max-width: 1920px) {
      width: 284px;
      height: 191px;
    }
    @media (max-width: 1440px) {
      width: 262px;
      height: 176px;
    }
    @media (max-width: 1280px) {
      width: 268px;
      height: 180px;
    }
    @media (max-width: 1024px) {
      width: 239px;
      height: 161px;
    }
    @media (max-width: 834px) {
      width: 298px;
      height: 201px;
    }
    @media (max-width: 744px) {
      width: 391px;
      height: 264px;
    }
    @media (max-width: 430px) {
      width: 307px;
      height: 208px;
    }
    @media (max-width: 375px) {
      width: 261px;
      height: 177px;
    }
  }
  &__label {
    display: inline-block;
    position: absolute;
    font-size: 14px;
    font-weight: 600;
    line-height: 120%;
    padding: 4px 16px;
    border-radius: 14px;
    color: $main-background-color;
    @media (max-width: 1920px) {
      font-size: 12px;
    }
    @media (max-width: 1024px) {
      font-size: 10px;
    }
    @media (max-width: 834px) {
      font-size: 14px;
    }
    @media (max-width: 430px) {
      font-size: 10px;
    }
    &_top {
      left: 8px;
      top: 8px;
      background-color: $green-color;
    }
    &_sale {
      top: 8px;
      left: 50%;
      transform: translate(-50%, 0%);
      background-color: $orange-color;
    }
    &_popular {
      bottom: 8px;
      right: 8px;
      background-color: $violet-color;
    }
  }
  &__text {
    padding-top: 8px;
    line-height: 120%;
    font-size: 16px;
    span {
      font-weight: 600;
    }
    &_desc {
      overflow: hidden;
      text-overflow: ellipsis;
      display: -moz-box;
      -moz-box-orient: vertical;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      line-clamp: 2;
      @media (max-width: 430px) {
        -webkit-line-clamp: 1;
        -webkit-box-orient: vertical;
        line-clamp: 1;
      }
    }
    @media (max-width: 1920px) {
      font-size: 14px;
    }
    @media (max-width: 834px) {
      font-size: 16px;
    }
    @media (max-width: 430px) {
      &:first-of-type {
        padding-top: 4px;
      }
    }
    @media (max-width: 375px) {
      padding-top: 4px;
      &:first-of-type {
        padding-top: 2px;
      }
    }
  }
}
</style>
