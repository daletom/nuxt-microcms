<template>
  <div class="p-4">
    <Hero />
    <div class="flex flex-wrap">
      <div
        class="p-4 lg:w-1/3 md:w-1/2 sm:w-full"
        v-for="content in contents"
        :key="content.id"
      >
        <p class="text-2xl p-2" v-html="content.title"></p>
        <ix-img
          :src="imageSrc(content)"
          :imgixParams="{ fit: 'crop', ar: '1.8:1' }"
          sizes="(min-width: 1024px) calc(33vw - 60px), (min-width: 768px) calc(50vw - 100px), calc(100vw - 70px)"
          loading="lazy"
        />
        <p class="p-2" v-html="content.content"></p>
      </div>
    </div>
    <ul>
      <li v-for="content in contents" :key="content.id">
        {{ content.hero.url }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  async asyncData() {
    const { data } = await axios.get(
      // your-service-id部分は自分のサービスidに置き換えてください
      `https://${process.env.MICRO_PROJECT}.microcms.io/api/v1/blog`,
      {
        // your-api-key部分は自分のapi-keyに置き換えてください
        headers: { "X-API-KEY": `${process.env.MICRO_API}` },
      }
    );
    return data;
  },
  methods: {
    imageSrc(content) {
      return (new URL(content.hero.url)).pathname
    },
  },
};
</script>
