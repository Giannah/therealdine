<template>
  <div>
    <h1>Tous les articles</h1>
    <div>
      <ul
        class="block m-4 lg:grid lg:grid-flex-row lg:grid-cols-3 lg:grid-rows-3 lg:gap-x-4 lg:gap-y-8"
      >
        <li v-for="article of articles" :key="article.slug">
          <nuxt-link
            :to="{ name: 'blog-slug', params: { slug: article.slug } }"
          >
            <img :src="require(`~/assets/images/${article.img}`)" />
            <div>
              <h2 class="inline">
                {{ article.title }}
              </h2>
              <p class="inline">par {{ article.author.name }}</p>
              <p>{{ article.description }}</p>
            </div>
          </nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'blog',
  async asyncData({ $content, params }) {
    const articles = await $content('articles', params.slug)
      .only(['title', 'description', 'img', 'slug', 'author'])
      .sortBy('createdAt', 'asc')
      .fetch()
    return {
      articles,
    }
  },
}
</script>
<style scoped>
h1 {
  font-weight: bold;
  font-size: 2rem;
  font-family: 'Josefin Sans', sans-serif;
  line-height: 3rem;
}
img {
  height: 150px;
  width: 80%;
}
</style>
