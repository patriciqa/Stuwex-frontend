<template>
  <div
    ref="scroll_container"
    @mousewheel="handleScroll"
    class="flex flex-row scroll-container"
  >
    <div
      v-for="(image, index) in images"
      :key="index"
      :class="[`figure-${index}`]"
      class="child"
    >
      <navigation></navigation>
      <div v-if="image.Category.length == 1">
        <section
          v-if="image.Size === 'large'"
          class="child image text-center text-bottom"
        >
          <div
            class="image-bg child"
            :style="{ backgroundImage: `url(${image.Link})` }"
          >
            <div class="image-aside">
              <h3 class="image-text">{{ image.Filetext }}</h3>
              <p class="image-caption">{{ image.Title }}</p>
              <nuxt-link v-if="image.Haschild" :to="`/${image.Category}`">
                <button class="btn">More</button>
              </nuxt-link>
            </div>
            <span class="image-copy">{{ image.Copyright }}</span>
          </div>
        </section>

        <section
          v-if="image.Size === 'medium'"
          class="image text-right text-top"
        >
          <div class="image-container">
            <div class="image-section">
              <img :src="image.Link" :alt="image.Name" class="image-src" />
              <span class="image-copy">{{ image.Copyright }}</span>
            </div>
          </div>
          <div class="image-aside">
            <h2 class="image-text">
              {{ image.Filetext }}
            </h2>
            <p class="image-caption">{{ image.Title }}</p>
            <nuxt-link v-if="image.Haschild" :to="`/${image.Category}`">
              <button class="btn">More</button>
            </nuxt-link>
          </div>
        </section>

        <section class="image text-left text-top" v-if="image.Size === 'small'">
          <div class="image-aside">
            <h2 class="image-text">{{ image.Filetext }}</h2>
            <p class="image-caption">{{ image.Title }}</p>
            <nuxt-link v-if="image.Haschild" :to="`/${image.Category}`">
              <button class="btn">More</button>
            </nuxt-link>
          </div>
          <div class="flex image-container">
            <div class="image-section">
              <img :src="image.Link" :alt="image.Name" class="image-src" />
              <span class="image-copy">{{ image.Copyright }}</span>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
    };
  },

  async created() {
    this.images = await this.$axios
      .get("http://bildarchivaarau.azurewebsites.net/api/photo")
      .then((res) => res.data.filter((e) => e.Category.length === 1));
  },

  methods: {
    handleScroll(e) {
      // this.$refs["scroll_container"].scrollLeft += e.deltaY;
      if (e.deltaY) {
        window.dispatchEvent(new WheelEvent("wheel", { deltaX: e.deltaY }));
      }
    },
  },
  beforeMount() {
    window.addEventListener("wheel", this.handleScroll);
  },

  beforeDestroy() {
    window.removeEventListener("wheel", this.handleScroll);
  },
};
</script>

<style>
.scroll-container {
  /* scroll-snap-type: both mandatory; */
}

.child {
  scroll-snap-align: end;
}
</style>