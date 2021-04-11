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
      <NuxtLink v-for="article in articles" :key="article.id" class="school" :to="'/articles/' + article.url">
        <Card :image="article.image" :title="article.title" :date="article.date" />
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
      articles: [
        {
          id: '1',
          title: 'Aktivity',
          url: 'aktivity',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          date: 'dnes'
        },
        {
          id: '2',
          title: 'Podujatia',
          url: 'podujatia',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          date: '1.4.2021'
        },
        {
          id: '2',
          title: 'Zameranie odborov',
          url: 'zameranie-odborov',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          date: '24.5.2020'
        }
      ]
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
