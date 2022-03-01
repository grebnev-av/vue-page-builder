<template>
  <div class="container">
    <Header
      :pageId="selectedProject.id"
    />
    <main class="main main_page">
      <div class="b-page">
        <component
          v-for="block in list"
          :key="block.id"
          :is="block.name"
          :id="block.id"
          :options="block.options"
          :styles="block.styles"
          :elements="block.elements"
        />
      </div>

      <div class="b-page__add" :class="{ '_active': isActive }">
        <div class="b-page__add-btn">
          <BaseButton
            text="Add"
            class="page-button _add"
            :class="{ '_active': isActive }"
            @click="handleShowBtn"
          />
          <BaseButton
            v-if="!isActive"
            text="Save"
            class="page-button _save"
            @click="save"
          />
        </div>
        <div class="b-page__add-blocks" v-if="isActive">
          <BaseButton
            class="b-page__add-blocks-btn"
            v-for="block in blocks"
            :text="`Add ${block.alias}`"
            :key="block.name"
            @click="clickAddBlock(block.name)"
          />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import { mapState, mapActions, mapMutations } from "vuex";
import Header from "../components/Header";

export default {
  name: "Page",
  components: {
    Header
  },
  data() {
    return {
      isActive: false
    };
  },
  computed: {
    ...mapState("Projects", [
      "selectedProject"
    ]),
    ...mapState("Pages", [
      "selectedPage"
    ]),
    ...mapState("Blocks", [
      "list",
      "blocks"
    ])
  },

  mounted() {
    this.setSelectedPage(this.$route.params.id);
    this.setSelectedPageId(this.$route.params.id);
  },

  methods: {
    ...mapActions("Projects", ["setSelectedProject"]),
    ...mapActions("Pages", ["setSelectedPage"]),
    ...mapActions("Blocks", ["setSelectedPageId"]),
    ...mapMutations("Blocks", ["setNewBlock"]),

    clickAddBlock(name) {
      this.isActive = false;
      this.setNewBlock(name);
    },

    handleShowBtn() {
      this.isActive = !this.isActive;
    },

    save() {
      this.$router.push(`/project/${this.selectedProject.id}`);
    }
  }
};
</script>

<style scoped lang="scss">
@import "../styles/variables";

.b-page {
  margin: 0 auto;
  width: 100%;
  padding-bottom: 60px;

  &__add {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 0;
    padding: 0;
    background-color: $orange;

    display: flex;
    justify-content: center;

    &._active {
      top: 6.8rem;
      bottom: 0;
      left: 0;
      right: 0;
      z-index: 20;
      padding: 4rem;
    }

    &-blocks-btn {
      margin: 0 0 2rem;
    }
  }
}

.page-button {
  min-width: auto;
  height: 64px;
  padding: 0;
  border-radius: 50%;
  transition: box-shadow $ease-in;

  &._add {
    position: fixed;
    right: 1rem;
    bottom: 2rem;
    width: 64px;
  }

  &._save {
    position: fixed;
    left: 1rem;
    bottom: 2rem;
    width: 64px;
  }

  &:after {
    display: none;
  }

  &._active {
    box-shadow: none;
    background: $black !important;
  }
}
</style>
