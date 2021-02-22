<template>
  <div class="flex flex-row flex-nowrap justify-between content-center">
    <div class="hover:text-yellow-500">
      <span v-if="prev"><fa icon="arrow-circle-left" class="mr-1" /></span>
      <nuxt-link
        v-if="prev"
        :to="{ name: 'blog-slug', params: { slug: prev.slug } }"
      >
        {{ prev.title }}
      </nuxt-link>
      <span v-else>&nbsp;</span>
    </div>
    <div class="hover:text-yellow-500">
      <nuxt-link
        v-if="next"
        :to="{ name: 'blog-slug', params: { slug: next.slug } }"
        >{{ next.title }}</nuxt-link
      >
      <span v-else>&nbsp;</span>
      <span v-if="next"><fa icon="arrow-circle-right" class="ml-1" /></span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    prev: {
      type: Object,
      default: () => null,
    },
    next: {
      type: Object,
      default: () => null,
    },
  },
}
</script>
