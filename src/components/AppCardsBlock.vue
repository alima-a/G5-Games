<template>
  <app-container>
    <div class="cards">
      <div v-for="(product, index) in products" :key="product.id">
        <app-card :product="product" :index="index" />
      </div>
    </div>
  </app-container>
</template>

<script>
import AppContainer from "@/components/AppContainer";
import AppCard from "@/components/AppCard";
export default {
  name: "AppCardsBlock",
  components: { AppCard, AppContainer },
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style scoped lang="scss">
.cards {
  display: flex;
  flex-wrap: wrap;
  height: 100%;
  width: 100%;
  padding-top: 26px;
  justify-content: space-between;
  @media (max-width: 1920px) {
    padding-top: 24px;
  }
  @media (max-width: 1280px) {
    padding-top: 16px;
  }
  @media (max-width: 1024px) {
    padding-top: 25px;
  }
  @media (max-width: 834px) {
    padding-top: 16px;
  }
  @media (max-width: 430px) {
    padding-top: 32px;
  }
  @media (max-width: 375px) {
    padding-top: 8px;
  }
}
</style>
