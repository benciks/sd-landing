<template>
  <section class="train">
    <div class="container">
      <img src="@/static/metro.svg" alt="Metro illustration">
      <div class="content">
        <h3 class="order-2 bold">
          {{ post.title }}
        </h3>
        <p class="copy-l">
          {{ post.description }}
        </p>
        <NuxtLink to="/articles/zameranie-odborov">
          <SButton value="Zobraziť odbory" type="textMore" />
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      post: {
        title: 'Vlaková doprava',
        description: 'Saw them. Moveth abundantly don\'t sea us i greater. Don\'t one cattle their i tree is fruitful whales morting abundantly to Our.'
      }
    }
  }
})
</script>

<style scoped lang="sass">
section.train
  padding: 10rem 0
  background: $ui6

  .container
    max-width: 90%
    margin: 0 auto

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
  section.train
    .container
      max-width: 90rem
      display: flex
      flex-direction: row-reverse
      align-items: center

      img
        max-width: 47.2rem

      .content
        margin-right: 4.7rem
        max-width: 38rem
</style>
