<template>
  <div>
    <h1>{{ articles[0].author.name }}</h1>
    <p>{{ articles[0].author.bio }}</p>
    <nuxt-link to="/blog/"><p>Tous les articles</p></nuxt-link>
    <h3>Plus d'articles:</h3>
    <ul>
      <li v-for="article in articles" :key="article.slug">
        <nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug } }">
          <img
            :src="article.img"
            :alt="require(`~/assets/images/${article.img}`)"
          />
          <div>
            <h2>{{ article.title }}</h2>
            <p>{{ article.description }}</p>
            <p>{{ formatDate(article.updatedAt) }}</p>
          </div>
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('articles', params.slug)
      .where({
        'author.name': {
          $regex: [params.author, 'i'],
        },
      })
      .without('body')
      .sortBy('createdAt', 'asc')
      .fetch()

    return {
      articles,
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('fr', options)
    },
  },
}
</script>
