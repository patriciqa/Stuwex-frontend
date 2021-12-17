<template>
  <main class="subpage">
    <navigation></navigation>
    <div class="category">
      <figure
        v-for="(image, index) in images"
        :key="index"
        :class="[`figure-${index}`]"
      >
        <div
          class="top-pages"
          v-if="image.Category.endsWith($route.params.Category)"
        >
          <section>
            <img
              :src="image.Link"
              :alt="image.Name"
              :id="[`image-${image.PhotoId}`]"
              :class="[`category--${image.Category}`, image.Size]"
            />
          </section>
          <figcaption>
            <p>{{ image.Title }}</p>
            <span>{{ image.Copyright }}</span>
          </figcaption>
        </div>
      </figure>
    </div>
    <button class="back-btn" @click="handleBack">
      <span class="arrow-up"
        ><img class="arrow-up-img" src="../assets/img/pfeil.svg" /></span
      >Zurück zur Startseite
    </button>
  </main>
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
      .get("https://bildarchivaarau.azurewebsites.net/api/photo")
      .then((res) =>
        res.data.filter(
          (e) =>
            e.Category.length === 2 &&
            e.Category.endsWith(this.$route.params.Category)
        )
      );
  },
  methods: {
    handleBack() {
      this.$router.go(-1);
    },
  },
};
</script>