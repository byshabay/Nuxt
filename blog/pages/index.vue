<template>
  <div class="home-page">
    <h2>Последние новости</h2>
    <div class="articles">
      <div class="article" v-for="article of articles" :key="article">

        <nuxt-link :to="{name: 'blog-slug', params: {slug: article.slug}}">
          <div class="article-inner">
            <img :src="require(`~/assets/resources/${article.img}`)" alt="" />
            <div class="detail">
              <h3>{{article.title}}</h3>
              <p>{{article.description}}</p>
            </div>
          </div>
        </nuxt-link>
      </div>

    </div>
  </div>
</template>

<script>
import TheHeader from '../components/TheHeader.vue';
export default {
    async asyncData( {$content, params} ) {
      const articles = await $content('blog', params.slug)
      .only(['title', 'description', 'slug', 'img'])
      .sortBy(['createdAt', 'asc'])
      .fetch();

    return {
      articles
    }
    }
}
</script>
