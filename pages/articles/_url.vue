<template>
  <div class="article">
    <div class="title">
      <div class="order-2 name">
        {{ article.name }}
      </div>
      <div>
        <CalendarIcon />
        <div class="copy-m">
          {{ normalizeDate(article.updatedAt) }}
        </div>
      </div>
    </div>
    <div class="image">
      <img :src="article.img" alt="Article image">
    </div>
    <div class="content" v-html="article.content" />
  </div>
</template>

<script>
import Vue from 'vue'
import { CalendarIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    CalendarIcon
  },
  data () {
    return {
      article: {}
    }
  },
  head () {
    return {
      title: `Študuj Dopravu - ${this.article.name}`
    }
  },
  beforeMount () {
    this.getArticle()
  },
  methods: {
    async getArticle () {
      const articleUrl = '/articles/' + this.$route.params.url
      const res = await this.$axios.get(articleUrl)

      if (typeof res.data === 'object') {
        this.article = res.data
      } else {
        this.$nuxt.error({ statusCode: 404 })
      }
    },
    normalizeDate (date) {
      const normalDate = new Date(date)
      return normalDate.getDate() + '.' + (normalDate.getMonth() + 1) + '.' + normalDate.getFullYear()
    }
  }
})
</script>

<style scoped lang="sass">
.article
  max-width: 68rem
  margin: 0 auto
  padding-top: 15.7rem

  .title
    width: 90%
    margin: 0 auto $xl auto

    div
      display: flex
      align-items: center

      div
        color: $ui3

      svg
        height: 18px
        width: 18px
        color: $ui3
        margin-right: $xs

    .name
      margin-bottom: $xs

  .image
    width: 90%
    max-width: 68rem
    height: 24.6rem
    margin: 0 auto

    img
      height: 100%
      width: 100%
      object-fit: cover
      border-radius: 8px

  .content
    width: 90%
    max-width: 68rem
    margin: $xxl auto 10rem auto

    ::v-deep h3
      @extend %order-3
      @extend %bold

      margin-bottom: $l

    ::v-deep p
      @extend %copy-l
      line-height: 3.57rem

</style>
