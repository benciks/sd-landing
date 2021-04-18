<template>
  <div>
    <div class="row">
      <div class="welcome">
        <img src="@/static/walking.svg" alt="Walking illustration">
        <h1 class="order-3 bold">
          Vitajte, {{ loggedInUser.name.replace(/ .*/, '') }}
        </h1>
        <p class="copy-m">
          {{ welcome.description }}
        </p>
        <NuxtLink to="/">
          <SButton value="Zobraziť stránku" type="textMore" />
        </NuxtLink>
        <div />
      </div>
      <div class="edited">
        <NuxtLink v-for="article in filteredArticles" :key="article.url" :to="'/admin/articles/' + article.url">
          <div class="article">
            <div class="head">
              <p class="copy-l bold">
                {{ article.name }}
              </p>
              <p class="copy-s date">
                {{ normalizeDate(article.updatedAt) }}
              </p>
            </div>
            <p class="copy-m description">
              {{ article.description }}
            </p>
            <div class="details">
              <p class="copy-s">
                {{ article.author }}
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
            </div>
          </div>
        </NuxtLink>
      </div>
    </div>
    <div class="stats">
      <div class="title">
        <ActivityIcon />
        <p class="copy-m bold">
          Štatistiky
        </p>
      </div>
      <div class="counters">
        <NuxtLink to="/admin/schools">
          <div class="schoolcount">
            <div>
              <BookIcon />
              <p class="copy-s bold">
                Školy
              </p>
            </div>
            <h3 class="order-2">
              {{ schoolCount }}
            </h3>
          </div>
        </NuxtLink>
        <NuxtLink to="/admin/articles">
          <div class="articlecount">
            <div>
              <PaperclipIcon />
              <p class="copy-s bold">
                Články
              </p>
            </div>
            <h3 class="order-2">
              {{ articleCount }}
            </h3>
          </div>
        </NuxtLink>
        <NuxtLink to="/admin/users">
          <div class="usercount">
            <div>
              <UsersIcon />
              <p class="copy-s bold">
                Používatelia
              </p>
            </div>
            <h3 class="order-2">
              {{ userCount }}
            </h3>
          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { mapGetters } from 'vuex'
import { ActivityIcon, BookIcon, PaperclipIcon, UsersIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    ActivityIcon,
    BookIcon,
    PaperclipIcon,
    UsersIcon
  },
  layout: 'admin',
  middleware: 'auth',
  data () {
    return {
      welcome: {
        description: 'V administrátorskej časti môžete opravovať články, podujatia, obsah stránok a tak ďalej.'
      },
      schools: [],
      users: [],
      articles: [],
      stats: {
        schools: '32',
        articles: '19',
        users: '1'
      }
    }
  },
  computed: {
    ...mapGetters(['loggedInUser']),
    schoolCount () {
      return this.schools.length
    },
    articleCount () {
      return this.articles.length
    },
    userCount () {
      return this.users.length
    },
    filteredArticles () {
      const articles = this.articles

      const sorted = articles.sort(function (el) {
        return new Date() - new Date(el.updatedAt)
      })

      return sorted.slice(0, 4)
    }
  },
  beforeMount () {
    this.fetchSchools()
    this.fetchArticles()
    this.fetchUsers()
  },
  methods: {
    async fetchSchools () {
      this.schools = await this.$axios.$get('/schools')
    },
    async fetchArticles () {
      this.articles = await this.$axios.$get('/articles')
    },
    async fetchUsers () {
      this.users = await this.$axios.$get('/users')
    },
    normalizeDate (date) {
      const normalDate = new Date(date)
      return normalDate.getDate() + '.' + (normalDate.getMonth() + 1) + '.' + normalDate.getFullYear()
    }
  }
})
</script>

<style scoped lang="sass">
.row
  display: flex

  .edited
    margin-left: $m
    margin-top: $xl
    width: 43.7rem

    a
      text-decoration: none

      &:last-child
        .article
          margin-bottom: 0

.welcome
  background: $white
  border-radius: 6px
  border: 1px solid $ui5
  max-width: 44.2rem
  padding: $xl
  margin-top: $xl
  display: flex
  flex-direction: column
  justify-content: center

  h1
    margin: $xl 0 $xs 0

  p
    margin-bottom: $xl
    color: $ui2

  a
    text-decoration: none

.article
  background: $white
  border: 1px solid $ui5
  border-radius: 6px
  padding: $l
  margin-bottom: $s

  .description
    color: $ui3
    overflow: hidden
    display: -webkit-box
    -webkit-line-clamp: 2
    -webkit-box-orient: vertical

  .head
    display: flex
    justify-content: space-between
    align-items: center
    margin-bottom: $xs

    .date
      color: $ui3

  .details
    display: flex
    justify-content: space-between
    align-items: center
    margin-top: 3rem

    p
      color: $ui3

    .status
      padding: $xxs $s
      border-radius: 99em

    .published
      background: $green

      p
        color: $white

    .unpublished
      background: $ui5

.stats
  margin-top: $xl

  .title
    display: flex
    align-items: center
    margin-bottom: $m

    svg, p
      color: $ui3

    svg
      height: 18px
      width: 18px
      margin-right: $xs

.counters
  display: flex
  justify-content: space-between
  a
    text-decoration: none

    .schoolcount, .articlecount, .usercount
      width: 29.2rem
      padding: $l
      border-radius: 8px

      div
        display: flex
        align-items: center

        svg
          height: 18px
          width: 18px
          margin-right: $xxs

      h3
        margin-top: $xs

    .schoolcount
      background: $primary

      p, svg, h3
        color: $white

    .articlecount
      background: $tertiary

      p, svg, h3
        color: $ui2

    .usercount
      background: $secondary

      p, svg, h3
        color: $ui2
</style>
