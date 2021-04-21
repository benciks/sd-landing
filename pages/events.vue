<template>
  <div>
    <div class="hero">
      <div>
        <div class="text">
          <h1 class="order-1 bold">
            Podujatia
          </h1>
          <p class="copy-l">
            Saw them. Moveth abundantly don't sea us i greater. Don't one cattle their i tree is fruitful whales morting abundantly to Our.
          </p>
        </div>
        <img src="@/static/travel.svg" alt="Travel illustration">
      </div>
    </div>
    <div class="content" v-html="article.content" />
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      article: {}
    }
  },
  head () {
    return {
      title: 'Študuj Dopravu - Podujatia'
    }
  },
  beforeMount () {
    this.getEvents()
  },
  methods: {
    async getEvents () {
      this.article = await this.$axios.$get('/articles/podujatia')
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

.content
  max-width: 90rem
  width: 90%
  margin: 8rem auto 0 auto

  ::v-deep h3
    @extend %order-3
    @extend %bold

    margin-bottom: $l

  ::v-deep p
    @extend %copy-l
    line-height: 3.57rem

</style>
