<template>
  <AppNav></AppNav>
  <div class="container">
    <router-view />
  </div>
</template>

<script>
import AppNav from "@/components/AppNav";
import "@/assets/styles/common.scss";

export default {
  name: "App",
  components: {
    AppNav,
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";

.container {
  width: 100%;
  max-width: $sm;
  margin: 0 auto;

  @include sm {
    max-width: $sm;
  }

  @include lg {
    max-width: $md;
  }
}
</style>
