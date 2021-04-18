<template>
  <section class="hero">
    <div class="container">
      <div class="content">
        <h1 class="order-1 bold">
          {{ hero.title }}
        </h1>
        <p class="copy-l">
          {{ hero.description }}
        </p>
        <NuxtLink to="/events">
          <SButton value="Zistiť viac" />
        </NuxtLink>
      </div>
      <img src="@/static/airport.svg" alt="Airport illustration">
    </div>
  </section>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      hero: {
        title: 'Perspektíva, stabilita, uplatnenie',
        description: 'Saw them. Moveth abundantly don\'t sea us i greater. Don\'t one cattle their i tree is fruitful whales morting abundantly to Our.'
      }
    }
  }
})
</script>

<style scoped lang="sass">
section.hero
  background: $ui6
  padding-top: 20.4rem

  .container
    max-width: 90rem
    margin: 0 auto

    img
      width: 100%
      height: auto
      margin-top: 7.5rem

    .content
      text-align: center
      max-width: 90%
      margin: 0 auto
      display: flex
      flex-direction: column
      align-items: center

      p
        margin: $l 0 $xl 0
        color: $ui2

      a
        text-decoration: none

@media screen and (min-width: 768px)
  section.hero
    padding-top: 24.3rem

    .container
      img
        margin-top: 9.6rem

      .content
        max-width: 60rem

</style>
