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
        <div v-for="article in articles" :key="article.title" class="article">
          <div class="head">
            <p class="copy-l bold">
              {{ article.title }}
            </p>
            <p class="copy-s date">
              {{ article.lastEdited }}
            </p>
          </div>
          <p class="copy-m description">
            {{ article.description }}
          </p>
          <div class="details">
            <p class="copy-s">
              {{ article.author }}
            </p>
            <div class="div copy-s status">
              {{ article.status }}
            </div>
          </div>
        </div>
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
              {{ stats.schools }}
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
              {{ stats.articles }}
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
              {{ stats.users }}
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
      articles: [
        {
          title: 'Podujatia',
          lastEdited: '12.3.2021',
          description: 'Dni kariérového poradenstva Kam po skončení základnej školy - Študuj dopravu sa v roku 2020 neuskutočnili...',
          author: 'Simon Bencik',
          status: 'Nepublikované'
        },
        {
          title: 'Aktivity',
          lastEdited: '12.3.2021',
          description: 'Dni kariérového poradenstva Kam po skončení základnej školy - Študuj dopravu sa v roku 2020 neuskutočnili...',
          author: 'Simon Bencik',
          status: 'Publikované'
        },
        {
          title: 'Zameranie odborov',
          lastEdited: '12.3.2021',
          description: 'Dni kariérového poradenstva Kam po skončení základnej školy - Študuj dopravu sa v roku 2020 neuskutočnili...',
          author: 'Simon Bencik',
          status: 'Nepublikované'
        }
      ],
      stats: {
        schools: '32',
        articles: '19',
        users: '1'
      }
    }
  },
  computed: {
    ...mapGetters(['loggedInUser'])
  }
})
</script>

<style scoped lang="sass">
.row
  display: flex

  .edited
    margin-left: $m
    margin-top: $xl
    max-width: 43.7rem

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
  margin-bottom: $m

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
      background: $secondary
      padding: $xxs $s
      border-radius: 99em
      color: $ui2

.article:last-of-type
  margin-bottom: 0

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
