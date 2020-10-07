<template>
  <b-card
    body-class="d-flex flex-column flex-lg-row"
    :class="featured == true ? 'border-left-4' : 'border-0'"
    class="shadow-sm bg-white rounded mb-6 mt-16 mt-lg-8"
  >
    <!-- Image goes here -->
    <div class="mb-2 mb-lg-0">
      <img class="mt-n16 mt-lg-0" v-bind:src="require('../assets' + img)" />
    </div>

    <!-- Description goes here -->
    <div class="d-flex flex-column ml-2 ml-lg-4 ">
      <h6 class="text-dark-cyan">
        {{ company }}
        <span
          class="rounded-pill bg-dark-cyan text-white m-2 py-1 px-2 text-sm text-uppercase"
          v-if="isNew == true"
          >New</span
        >
        <span
          class="rounded-pill bg-dark text-white m-2 py-1 px-2 text-sm text-uppercase"
          v-if="featured == true"
          >Featured</span
        >
      </h6>
      <h5 role="button" class="py-2 py-lg-0 position">{{ position }}</h5>
      <p class="text-muted">{{ postedAt }} · {{ contract }} · {{ location }}</p>
    </div>
    <!-- Tags item goes here -->
    <div
      class="d-flex flex-wrap align-items-center border-top-1 border-lg-top-0 pt-4 ml-2 mt-2 mt-lg-0 ml-lg-auto"
    >
      <div
        :v-if="tag !== null"
        :key="tag"
        v-for="tag in tags"
        class="mr-2 mb-4"
      >
        <span
          @click="onHandleClick(tag)"
          role="button"
          class="bg-light-cyan text-dark-cyan text-center p-2 tag-item font-weight-bold"
          >{{ tag }}</span
        >
      </div>
    </div>
  </b-card>
</template>

<script>
export default {
  computed: {
    tags() {
      let allElement = [
        this.role,
        this.level,
        ...this.languages,
        ...this.tools,
      ];

      return allElement;
    },
  },
  methods: {
    onHandleClick(str) {
      this.$emit("clicked-show-detail", str);
    },
  },
  props: {
    company: {
      type: String,
    },
    position: {
      type: String,
    },
    isNew: {
      default: false,
      type: Boolean,
    },
    featured: {
      default: false,
      type: Boolean,
    },

    location: { type: String },
    contract: { type: String },
    postedAt: { type: String },
    role: { type: String },
    level: { type: String },
    languages: { type: Array },
    tools: { type: Array },
    img: {
      type: String,
    },
  },
};
</script>

<style></style>
