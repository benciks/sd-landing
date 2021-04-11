<template>
  <div class="article">
    <div class="title">
      <div class="order-2 name">
        {{ article.title }}
      </div>
      <div>
        <CalendarIcon />
        <div class="copy-m">
          {{ article.date }}
        </div>
      </div>
    </div>
    <div class="image">
      <img :src="article.image" alt="Article image">
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
      article: {
        id: '1',
        title: 'Aktivity',
        url: 'aktivity',
        image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
        date: 'dnes',
        content: '<h3>O podujatí</h3><p>Rezort dopravy a výstavby má snahu motivovať žiakov základných škôl k štúdiu na stredných odborných školách a následne k výberu povolania v oblasti dopravy, k rozvíjaniu a prehlbovaniu ich záujmu o zvolené povolanie a budovaniu ich vzťahu k budúcej profesii, a to najmä prostredníctvom organizovania zážitkových aktivít.\n</p>'
      }
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
