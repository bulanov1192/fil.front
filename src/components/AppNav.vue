<template>
  <nav>
    <router-link class="logo" to="/">
      <div></div>
      <span>Список студентов</span>
    </router-link>
    <a rel="noopener" class="add-btn">
      <span>Добавить студента</span>
      <div></div>
    </a>
  </nav>
</template>

<script>
export default {
  name: "AppNav",
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";

$nav-height: 60px;

nav {
  width: 100%;
  background: #fff;
  @include setProperty(height, 40px, 48px, 56px, 60px);
  display: flex;
  justify-content: space-between;
  align-items: center;

  @include xs {
    box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.3);
  }
}

.logo {
  height: 100%;
  text-decoration: none;
  color: #000;
  display: flex;
  justify-content: flex-start;
  align-items: center;

  div {
    display: block;
    height: 100%;
    @include setProperty(width, 40px, 48px, 56px, 60px);
    background-image: url("@/assets/icons/students.svg");
    background-repeat: no-repeat;
    background-size: 50%;
    background-position: center;
  }

  span {
    @include setProperty(font-size, 12px, 12px, 14px, 16px);
  }
}

.add-btn {
  @include setProperty(padding, 0, 8px 10px, 8px 12px, 10px 14px);
  @include setProperty(font-size, 12px, 12px, 14px, 16px);
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: auto;
  outline: none;
  text-decoration: none;
  border-radius: $common-corner;
  cursor: pointer;
  margin-right: 8px;

  span {
    display: none;

    @include sm {
      display: inline;
    }
  }

  div {
    @include setProperty(width, 16px, 12px, 14px, 16px);
    @include setProperty(height, 16px, 12px, 14px, 16px);
    background-image: url("@/assets/icons/plus.svg");
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    margin: 8px;

    @include sm {
      margin: 0 0 0 8px;
    }
  }

  @include sm {
    border: 1px solid #dadada;

    &:hover {
      background-color: rgba(#ddd, 0.3);
    }
  }

  &:active {
    background-color: rgba(#ddd, 0.5);
  }
}
</style>
