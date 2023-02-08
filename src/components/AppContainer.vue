<template>
  <div class="container"><slot /></div>
</template>

<script>
export default {
  name: "AppContainer",
};
</script>
<style scoped lang="scss">
.container {
  width: 100%;
  height: 100%;
  max-width: 1386px;
  margin: 0 auto;
  // padding: 0 8px;
  @media (max-width: 1920px) {
    max-width: 1290px;
  }
  @media (max-width: 1440px) {
    max-width: 1194px;
  }
  @media (max-width: 1280px) {
    max-width: 906px;
  }
  @media (max-width: 1024px) {
    max-width: 816px;
  }
  @media (max-width: 834px) {
    max-width: 658px;
  }
  @media (max-width: 744px) {
    max-width: 412px;
  }
  @media (max-width: 430px) {
    max-width: 324px;
  }
  @media (max-width: 375px) {
    max-width: 276px;
  }
}
</style>
