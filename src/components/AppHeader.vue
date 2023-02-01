<template>
  <header>
    <img src="" alt="logo" />
    <app-button />
  </header>
</template>

<script>
import AppButton from "@/components/AppButton";
export default {
  name: "AppHeader",
  components: { AppButton },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
