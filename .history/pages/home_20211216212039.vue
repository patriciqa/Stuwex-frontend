<template>
  <main class="home">
    <navigation></navigation>
    <div ref="scroll_container" class="flex flex-row scroll-container">
      <div
        v-for="(image, index) in images"
        :key="index"
        :class="[`figure-${index}`]"
      >
        <div v-if="image.Category.length == 1">
          <section
            v-if="image.Size === 'large'"
            class="image text-center text-bottom"
          >
            <div
              class="image-bg"
              :style="{ backgroundImage: `url(${image.Link})` }"
              :class="index % 2 == 0 ? 'red-bg' : ''"
            >
              <div class="image-aside">
                <h3 class="image-text" :class="index % 2 == 0 ? '' : 'black-font'">
                  {{ image.Filetext }}
                </h3>
                <p class="image-caption">{{ image.Title }}</p>
                <nuxt-link
                  class="link"
                  v-if="image.Haschild"
                  :to="`/${image.Category}`"
                >
                  <span class="arrow-down"
                    ><img
                      class="arrow-down-img"
                      src="../assets/img/pfeil.svg" /></span
                  >Mehr ansehen
                </nuxt-link>
              </div>
              <span class="image-copy">{{ image.Copyright }}</span>
            </div>
          </section>

          <!-- <section
            v-if="image.Size === 'medium'"
            class="image text-right text-top reverse"
            :class="index % 2 == 0 ? 'reverse' : ''"
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
              <nuxt-link
                class="link"
                v-if="image.Haschild"
                :to="`/${image.Category}`"
              >
                <span class="arrow-down"
                  ><img
                    class="arrow-down-img"
                    src="../assets/img/pfeil.svg" /></span
                >Mehr ansehen
              </nuxt-link>
            </div>
          </section> -->

          <!-- <section
            class="image text-left text-top"
            :class="index % 2 == 0 ? 'reverse' : ''"
            v-if="image.Size === 'small'"
          >
            <div class="image-aside">
              <h2 class="image-text">{{ image.Filetext }}</h2>
              <p class="image-caption">{{ image.Title }}</p>
              <nuxt-link
                class="link"
                v-if="image.Haschild"
                :to="`/${image.Category}`"
              >
                <span class="arrow-down"
                  ><img
                    class="arrow-down-img"
                    src="../assets/img/pfeil.svg" /></span
                >Mehr ansehen
              </nuxt-link>
            </div>
            <div class="flex image-container">
              <div class="image-section">
                <img :src="image.Link" :alt="image.Name" class="image-src" />
                <span class="image-copy">{{ image.Copyright }}</span>
              </div>
            </div>
          </section> -->
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Vue from "vue";
export default {
  data() {
    return {
      images: [],
    };
  },

  async created() {
    this.images = await this.$axios
      .get("https://bildarchivaarau.azurewebsites.net/api/photo")
      .then((res) => res.data.filter((e) => e.Category.length === 1));
    Vue.nextTick(this.scrollAnimation);
  },
  methods: {
    scrollAnimation() {
      gsap.registerPlugin(ScrollTrigger);

      let sections = this.$refs.scroll_container.children;
      console.log(sections);
      gsap.to(sections, {
        xPercent: -100 * (sections.length - 1),
        ease: "none",
        scrollTrigger: {
          trigger: ".scroll-container",
          pin: true,
          scrub: 1,
          snap: 1 / (sections.length - 1),
          // base vertical scrolling on how wide the container is so it feels more natural.
          //end: "+=3500",
          end: () =>
            "+=" + document.querySelector(".scroll-container").offsetWidth,
        },
      });
    },
  },
};
</script>

<style scoped>
</style>