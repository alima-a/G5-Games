<template>
  <button class="button" @click="$emit('clickButton')">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "AppButton",
  props: {
    text: String,
  },
};
</script>
<style scoped lang="scss">
.button {
  border: none;
  padding: 8px 16px;
  background: $main-background-color;
  color: $second-font-color;
  border-radius: 100px;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  cursor: pointer;
  @media (max-width: 1920px) {
    font-size: 13px;
    line-height: 16px;
  }
  @media (max-width: 1440px) {
    font-size: 14px;
    line-height: 17px;
  }
  @media (max-width: 1024px) {
    font-size: 15px;
    line-height: 18px;
  }
  @media (max-width: 834px) {
    display: none;
  }
  &:hover {
    opacity: 0.9;
  }
}
</style>
