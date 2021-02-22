<template>
  <article class="text-justify m-4">
    <h1 class="title">{{ article.title }}</h1>
    <p class="mb-4 text-sm">{{ article.description }}</p>
    <img
      class="illustration lg:object-cover md:object-contain w-full m-3.5"
      :src="require(`~/assets/images/${article.img}`)"
      :alt="article.alt"
    />
    <p class="italic text-xs my-4">
      Dernière mise à jour : {{ formatDate(article.updatedAt) }}
    </p>
    <nav
      v-if="article.toc.length !== 0"
      class="article-nav m-4 p-5 lg:w-1/3 rounded-md bg-gray-100 sm:w-full md:w-full"
    >
      <h3 class="font-semibold text-md">Dans cet article</h3>
      <ul class="text-sm">
        <li v-for="link of article.toc" :key="link.id">
          <fa icon="arrow-right" class="ml-2.5 h-2 align-middle" />
          <nuxt-link :to="`#${link.id}`" class="p-2 hover:text-yellow-500">{{
            link.text
          }}</nuxt-link>
        </li>
      </ul>
    </nav>
    <nuxt-content :document="article" />
    <author :author="article.author" />
    <prev-next :prev="prev" :next="next" />
  </article>
</template>
<script>
export default {
  layout: 'blog',
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()

    return { article, prev, next }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('fr', options)
    },
  },
}
</script>
<style>
.title {
  font-weight: bold;
  font-size: 2rem;
  font-family: 'Josefin Sans', sans-serif;
  line-height: 3rem;
}
.nuxt-content h2 {
  font-size: 1.2rem;
  font-family: 'Josefin Sans', sans-serif;
  font-weight: bold;
  margin-top: 1rem;
}

.icon .icon-link {
  background-image: url('~assets/icons/star.svg');
  display: inline-block;
  height: 20px;
  width: 20px;
  background-size: 20px 20px;
}

.illustration {
  height: 450px;
}

@media screen and (min-width: 280px) and (max-width: 540px) {
  .illustration {
    height: 200px;
  }
  .article-nav {
    display: none;
  }
}
</style>
