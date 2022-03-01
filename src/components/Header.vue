<template>
  <header class="header" :class="{ '_active': isActive }" :isActive="isActive">
    <div class="header__logo">
      <router-link to="/" class="header__logo-link">
        <IconLogo class="header__logo-icon" />
      </router-link>
    </div>
    <nav class="header__menu">
      <ul class="header__menu-list">
        <li class="header__menu-item" @click="onGoTo(`/projects`)">
          <BaseLink
            href="/projects"
            text="My projects"
            class="header__menu-link linkHeader"
          />
        </li>
        <li class="header__menu-item" v-if="pageId !== 0" @click="onGoTo(`/project/${pageId}`)">
          <BaseLink
            :href="`/project/${pageId}`"
            text="My pages"
            class="header__menu-link linkHeader"
          />
        </li>
      </ul>
    </nav>
    <div class="header__controls">
      <BaseButton
        class="burger header__controls-toggle"
        @click="onBurgerClick"
      />
    </div>
  </header>
</template>

<script>
import { mapState } from 'vuex'
import IconLogo from "../assets/icons/logo.svg";

export default {
  name: "Header",
  components: { IconLogo },
  data: () => ({
    isActive: false
  }),
  props: {
    pageId: {
      type: Number,
      default: 0
    }
  },
  computed: {
    ...mapState('User', ['isAuth', 'user']),
  },
  methods: {
    onBurgerClick() {
      this.isActive = !this.isActive;
    },
    onGoTo(url) {
      this.isActive = false;
      this.$router.push(url);
    }
  }
};
</script>

<style scoped lang="scss">
@import "../styles/variables";
.header {
  $this: &;
  position: fixed;
  z-index: 10;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  padding: 30px 2vw;
  justify-content: center;
  align-items: center;
  box-shadow: 0 5px 15px rgba($gray5, 0.15);
  &._active {
    bottom: 0;
    background: $orange;
    align-items: flex-start;
  }

  @media (max-width: $desktop) {
    padding: 17px 2vw;
  }

  @media (max-width: $mobile) {
    padding: 20px 3.5vw;
    background: transparent;
    box-shadow: none;
  }

  &__logo {
    position: relative;
    z-index: 1;
    padding: 0 3.5vw 0 1vw;
  }

  &__logo-link {
    display: inline-block;
    vertical-align: middle;
    font-size: 0;
    fill: $white;

    @media (max-width: $mobile) {
      fill: $black;
    }

    > svg {
      vertical-align: middle;
    }

    #{$this}._active & {
      fill: $white;
    }
  }

  &__logo-icon {
    width: 120px;
    height: 45px;

    @media (max-width: $desktop) {
      width: 100px;
      height: 34px;
    }

    @media (max-width: $mobile) {
      width: 90px;
      height: 30px;
    }
  }

  &__menu {
    width: 100%;
    @media (max-width: $mobile) {
      pointer-events: none;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      z-index: -1;
      background-repeat: no-repeat;
      background-position: 50% 0;
      opacity: 0;
      transition: opacity 0ms ease-in;
    }

    .header[isActive] & {
      @media (max-width: $mobile) {
        z-index: 0;
        pointer-events: auto;
        opacity: 1;
        transition: opacity $ease-in;
      }
    }
  }

  &__menu-list {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 17rem 0 0;
    margin: 0;

    @media (max-width: $mobile) {
      flex-direction: column;
      padding: 65px 0 200px;
    }

    #{$this}._active & {
      margin: 4rem 0 0 auto;
    }
  }

  &__menu-item {
    margin: 0 2.35vw 0 2.5vw;

    @media (max-width: $tablet) {
      margin: 0 1.5vw;
    }

    @media (max-width: $mobile) {
      margin: 0 1.75vw 28px;
    }
  }

  &__menu-link {
    display: inline-block;
    vertical-align: middle;
    font-family: "Roboto", sans-serif;
    text-transform: uppercase;

    &--icon {
      margin: 10px 0 0;

      @media (max-width: $mobile) {
        display: flex;
        text-decoration: none;
        align-items: center;
        margin: 0;
      }

      &:hover .header__menu-link--mobile {
        background: $black-gray;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        opacity: 1;
      }
    }

    > svg {
      width: 38px;
      height: 38px;

      @media (max-width: $desktop) {
        width: 21px;
        height: 21px;
      }
    }

    &--mobile {
      display: none;

      @media (max-width: $mobile) {
        position: relative;
        display: inline-block;
        vertical-align: middle;
        padding: 0 10px 0 30px;
        color: $black;
        text-decoration: none;
        text-transform: none;
        font-weight: 600;
      }
    }
  }

  &__controls {
    display: flex;
    align-items: center;
    margin: 0 0 0 auto;
  }

  &__controls-button {
    @media (max-width: $mobile) {
      display: none;
    }
  }

  &__controls-toggle {
    display: none;

    @media (max-width: $mobile) {
      display: inline-block;
      vertical-align: middle;
    }
  }
}
</style>
