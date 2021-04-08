<template>
  <div class="articles">
    <div class="head">
      <h3 class="order-3 bold">
        Články
      </h3>
      <div>
        <SInput type="Search" placeholder="Hľadajte článok" class="search" />
        <SButton value="Pridať Článok" />
      </div>
    </div>
    <div class="columns">
      <p class="label">
        Názov
      </p>
      <p class="label author">
        Autor
      </p>
      <p class="label edited">
        Upravené
      </p>
      <p class="label status">
        Status
      </p>
    </div>
    <div class="items">
      <div v-for="article in articles" :key="article.id" class="item">
        <p class="copy-m bold">
          {{ article.title }}
        </p>
        <p class="author copy-m">
          {{ article.author }}
        </p>
        <p class="edited copy-m">
          {{ article.edited }}
        </p>
        <div v-if="article.status === 'published'" class="status published">
          <p class="copy-s">
            Publikované
          </p>
        </div>
        <div v-if="article.status === 'unpublished'" class="status unpublished">
          <p class="copy-s">
            Nepublikované
          </p>
        </div>
        <NuxtLink :to="'/admin/articles/' + article.id" class="more">
          <MoreVerticalIcon />
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { MoreVerticalIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    MoreVerticalIcon
  },
  layout: 'admin',
  middleware: 'auth',
  data () {
    return {
      articles: [
        {
          id: '1',
          title: 'Zameranie odborov',
          author: 'John doe',
          edited: 'today',
          status: 'published'
        },
        {
          id: '2',
          title: 'Aktivity',
          author: 'John doe',
          edited: 'yesterday',
          status: 'unpublished'
        },
        {
          id: '3',
          title: 'Podujatia',
          author: 'John doe',
          edited: 'today',
          status: 'published'
        }
      ]
    }
  }
})
</script>

<style scoped lang="sass">
.articles
  .head
    display: flex
    justify-content: space-between
    align-items: center
    margin-top: $xxl

    div
      display: flex

      .search
        width: 32rem
        margin-right: $s

  .items
    .item
      background: $white
      border: 1px solid $ui5
      border-bottom: 0
      padding: $m $l
      display: flex
      align-items: center
      position: relative

      .author
        position: absolute
        left: 306px

      .edited
        position: absolute
        left: 538px

      .status
        padding: $xxs $s
        position: absolute
        left: 729px
        border-radius: 99em

      .published
        background: $green

        p
          color: $white

      .unpublished
        background: $ui5

      .more
        position: absolute
        right: $l
        display: flex
        align-items: center

        svg
          color: $ui4
          height: 18px
          width: 18px

    .item:first-of-type
      border-radius: 8px 8px 0 0

    .item:last-of-type
      border-radius: 0 0 8px 8px
      border-bottom: 1px solid $ui5

  .columns
    display: flex
    padding-left: $l
    padding-bottom: $xs
    align-items: center
    position: relative
    margin-top: $xxl

    .author
      position: absolute
      left: 306px

    .edited
      position: absolute
      left: 538px

    .status
      position: absolute
      left: 729px

    p
      color: $ui4

</style>
