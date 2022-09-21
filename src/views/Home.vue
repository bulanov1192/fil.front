<template>
  <div class="content"></div>
</template>

<script>
export default {
  name: "HomeView",
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";

.content {
  @include setProperty(margin-top, 12px, 8px, 12px, 16px);

  @include xs {
    box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.3);
  }
}
</style>
