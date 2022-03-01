<template>
  <router-link 
    class="link" :to="href">
    {{ text }}
  </router-link>
</template>

<script>
export default {
  name: "BaseLink",
  props: {
    href: String,
    text: String
  }
};
</script>

<style scoped lang="scss">
.link {
  display: inline-block;
  position: relative;
  font-size: 22px;
  line-height: 24px;
  font-weight: 800;
  color: $black;
  text-decoration: none;
  border: $black3 1px solid;
  padding: 1rem 2rem;
  min-width: 14rem;

  @media (max-width: $desktop) {
    font-size: 14px;
    line-height: 19px;
  }

  &:hover {
    background: $orange;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    opacity: 1;
  }

  &.disabled {
    color: rgba($white, 0.5);
    pointer-events: none;
    cursor: default;
  }

  &.capital {
    text-transform: uppercase;
  }

  &.linkHeader {
    @media (max-width: $desktop) {
      font-size: 12px;
      line-height: 14px;
    }

    @media (max-width: $mobile) {
      color: $black;
      font-size: 18px;
      line-height: 21px;
      font-weight: 600;
      text-transform: none;
    }
  }
}
</style>
