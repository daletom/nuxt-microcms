<template>
  <ix-img
    :src="imageSrc(content)"
    :imgixParams="{ fit: 'crop', ar: '1.8:1' }"
    sizes="(min-width: 1024px) calc(33vw - 60px), (min-width: 768px) calc(50vw - 100px), calc(100vw - 70px)"
    loading="lazy"
  />
</template>

<script>
import VueImgix from "~/plugins/vue-imgix.js";
export default {
  props: {
    imgobject: {
      type: Object,
      default: null,
    },
    imgixParams: {
      type: String,
      default: null,
    },
  },
  name: "responsiveImage",
  methods: {
    imageSrc(content) {
      return (new URL(content.hero.url)).pathname
    },
  },
};
</script>
