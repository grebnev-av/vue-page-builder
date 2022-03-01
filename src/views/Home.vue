<template>
  <div class="container">
    <Header />
    <main class="main">
      <div class="b-user">
        <div class="b-user__row">
          {{ user.name }}
        </div>
        <div class="b-user__row">
          {{ user.email }}
        </div>
        <div class="b-user__row">
          <div class="b-project-header__btn">
            <BaseButton
              text="Go to projects"
              @click="$router.push('/projects')"
            />
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Header from "../components/Header";

export default {
  name: "Home",
  components: {
    Header
  },

  computed: {
    ...mapState('User', [
      'user',
    ]),
  },
};
</script>

<style scoped lang="scss">
  .b-user {
    min-height: 50vh;
    
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    & > div {
      &:first-child {
        font-size: 4rem;
      }
      margin: 1rem;
    }
  }
</style>
