<template>
  <nuxt-link :to="`/blog/author/${author.name}`">
    <div
      class="author-container mt-8 p-2 lg:mr-auto lg:ml-auto lg:w-1/2 md:w-full sm:w-full"
    >
      <h3 class="font-semibold text-center text-xl mt-2">
        À propos de l'auteur
      </h3>
      <div class="flex items-center justify-around p-4">
        <img
          :src="require(`~/assets/images/${author.photo}`)"
          alt="author"
          class="author-photo flex-1 w-1/3 mr-4"
        />
        <div class="flex-none w-2/3">
          <p class="font-medium text-lg">{{ author.name }}</p>
          <p class="text-sm italic">{{ author.bio }}</p>
        </div>
      </div>
    </div>
  </nuxt-link>
</template>
<script>
export default {
  props: {
    author: {
      type: Object,
      required: true,
    },
  },
}
</script>
<style scoped>
@media screen and (min-width: 280px) and (max-width: 540px) {
  .author-container {
    display: none;
  }
}
</style>
