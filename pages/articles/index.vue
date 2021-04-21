<template>
  <div>
    <div class="hero">
      <div>
        <div class="text">
          <h1 class="order-1 bold">
            Články
          </h1>
          <p class="copy-l">
            Saw them. Moveth abundantly don't sea us i greater. Don't one cattle their i tree is fruitful whales morting abundantly to Our.
          </p>
        </div>
        <img src="~/static/transport.svg" alt="Travel illustration">
      </div>
    </div>
    <div class="articles">
      <NuxtLink v-for="article in filteredArticles" :key="article.id" class="school" :to="'/articles/' + article.url">
        <Card :image="article.img" :title="article.name" :date="normalizeDate(article.updatedAt)" />
      </NuxtLink>
    </div>
    <LandingSectionEvents />
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      articles: []
    }
  },
  head () {
    return {
      title: 'Študuj Dopravu - Články'
    }
  },
  computed: {
    filteredArticles () {
      return this.articles.filter(article => article.status === 'published')
    }
  },
  beforeMount () {
    this.getArticles()
  },
  methods: {
    async getArticles () {
      this.articles = await this.$axios.$get('/articles')
    },
    normalizeDate (date) {
      const normalDate = new Date(date)
      return normalDate.getDate() + '.' + (normalDate.getMonth() + 1) + '.' + normalDate.getFullYear()
    }
  }
})

</script>
<style scoped lang="sass">
.hero
  padding-top: 20.4rem
  background: $ui6

  div
    max-width: 90rem
    margin: 0 auto

  img
    width: 100%
    margin-top: $xl

  .text
    max-width: 90%
    text-align: center
    display: flex
    align-items: center
    flex-direction: column
    margin: 0 auto

    p
      color: $ui2
      margin-top: 2rem
      max-width: 44rem

.articles
  margin: 8rem auto 0 auto
  display: flex
  flex-direction: column
  align-items: center

  a
    width: 90%
    text-decoration: none
    margin-bottom: $l

@media screen and (min-width: 900px)
  .articles
    max-width: 90rem
    margin: 8rem auto 10rem auto
    display: grid
    grid-template-columns: repeat(3, auto)

    a
      width: 28.4rem
</style>
