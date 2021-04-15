<template>
  <div class="articles">
    <div class="head">
      <h3 class="order-3 bold">
        Články
      </h3>
      <div>
        <SInput v-model="searchQuery" type="Search" placeholder="Hľadajte článok" class="search" />
        <NuxtLink to="/admin/articles/create">
          <SButton value="Pridať Článok" />
        </NuxtLink>
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
      <div v-for="article in filteredArticles" :key="article.url" class="item">
        <p class="copy-m bold">
          {{ article.name }}
        </p>
        <p class="author copy-m">
          {{ article.author }}
        </p>
        <p class="edited copy-m">
          {{ article.updatedAt }}
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
        <SDropdown class="more">
          <template #toggler>
            <MoreVerticalIcon />
          </template>
          <SDropdownContent>
            <NuxtLink :to="'/admin/articles/' + article.url" class="link">
              <EditIcon />
              <div class="copy-m">
                Upraviť článok
              </div>
            </NuxtLink>
            <div class="link" @click="deleteArticle(article.url)">
              <TrashIcon />
              <div class="copy-m">
                Zmazať článok
              </div>
            </div>
          </SDropdownContent>
        </SDropdown>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { MoreVerticalIcon, EditIcon, TrashIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    MoreVerticalIcon,
    EditIcon,
    TrashIcon
  },
  layout: 'admin',
  middleware: 'auth',
  data () {
    return {
      searchQuery: '',
      articles: []
    }
  },
  computed: {
    filteredArticles () {
      if (this.searchQuery) {
        return this.articles.filter((item) => {
          return item.name.startsWith(this.searchQuery) || item.author.startsWith(this.searchQuery)
        })
      } else {
        return this.articles
      }
    }
  },
  beforeMount () {
    this.fetchArticles()
  },
  methods: {
    async fetchArticles () {
      this.articles = await this.$axios.$get('/articles')
    },
    async deleteArticle (articleUrl) {
      const url = '/articles/' + articleUrl
      console.log(articleUrl)
      await this.$axios.$delete(url)
      await this.fetchArticles()
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

      a
        text-decoration: none

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
