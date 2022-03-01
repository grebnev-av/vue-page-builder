<template>
  <div id="app" class="app">
    <div class="app__container">
      <transition name="fade">
        <router-view />
      </transition>
    </div>
  </div>
</template>

<style lang="scss">
@import "styles/styles";
.app {
  display: flex;
  justify-content: center;
  width: 100%;
  background-color: $black3;
  &__container {
    position: relative;
    width: 100%;
    min-height: 100vh;
    margin: 0 auto;
    background-color: $gray2;
    @media (max-width: $mobile) {
      padding: 4rem 2rem 0;
      max-width: $mobile;
    }
  }
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>
