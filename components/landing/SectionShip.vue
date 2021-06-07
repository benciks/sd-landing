<template>
  <section class="ship">
    <img src="@/static/ship.svg" alt="Ship illustration">
    <div class="content">
      <h3 class="order-2 bold">
        {{ post.title }}
      </h3>
      <p class="copy-l">
        {{ post.description }}
      </p>
      <NuxtLink to="/articles/zamestnavatelia">
        <SButton value="Zobraziť viac" type="textMore" />
      </NuxtLink>
    </div>
  </section>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      post: {
        title: 'Zamestnávatelia',
        description: 'Saw them. Moveth abundantly don\'t sea us i greater. Don\'t one cattle their i tree is fruitful whales morting abundantly to Our.'
      }
    }
  }
})
</script>

<style scoped lang="sass">
section.ship
  max-width: 90%
  margin: 0 auto
  padding: 10rem 0

  img
    width: 100%
    height: auto
    margin-bottom: $xxl

  .content
    p
      margin: $xs 0 $l 0
      color: $ui2

    a
      text-decoration: none

@media screen and (min-width: 768px)
  section.ship
    max-width: 90rem
    display: flex
    align-items: center

    img
      max-width: 47.2rem

    .content
      margin-left: 4.7rem
      max-width: 38rem
</style>
