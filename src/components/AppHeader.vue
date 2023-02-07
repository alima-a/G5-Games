<template>
  <header class="main-header">
    <app-container class="main-header__container">
      <img
        class="main-header__logo"
        src="../assets/images/logo.png"
        alt="logo"
      />
      <app-button :text="'Update Products'" class="main-header__button" />
    </app-container>
  </header>
</template>

<script>
import AppButton from "@/components/AppButton";
import AppContainer from "@/components/AppContainer";
export default {
  name: "AppHeader",
  components: { AppContainer, AppButton },
};
</script>
<style scoped lang="scss">
.main-header {
  width: 100%;
  height: 48px;
  background-color: $second-background-color;
  &__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__logo {
    height: 20px;
    width: 20px;
    @media (max-width: 1920px) {
      height: 22px;
      width: 22px;
    }
    @media (max-width: 1440px) {
      height: 24px;
      width: 24px;
    }
    @media (max-width: 1280px) {
      height: 26px;
      width: 26px;
    }
    @media (max-width: 1024px) {
      height: 28px;
      width: 28px;
    }
    @media (max-width: 834px) {
      display: none;
    }
  }
}
</style>
