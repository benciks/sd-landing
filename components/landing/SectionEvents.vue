<template>
  <section class="events">
    <img src="@/static/waves.svg" alt="Waves">
    <div class="content">
      <h3 class="order-2 bold">
        {{ events.title }}
      </h3>
      <p class="copy-l">
        {{ events.description }}
      </p>
      <SButton value="Zobraziť podujatia" type="invert" />
    </div>
  </section>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      events: {
        title: 'Navštívte naše podujatie',
        description: 'Saw them. Moveth abundantly don\'t sea us i greater. Don\'t one cattle their i tree is fruitful whales morting abundantly to Our.'
      }
    }
  }
})
</script>

<style scoped lang="sass">
section.events
  max-width: 100rem
  margin: 0 auto
  position: relative

  img
    position: absolute
    width: 100%
    height: 100%
    object-fit: cover

  .content
    position: relative
    padding: 8rem 0
    max-width: 70%
    margin: 0 auto
    text-align: center
    display: flex
    flex-direction: column
    align-items: center

    h3
      color: $white

    p
      color: $ui4
      margin: $xs 0 $xl 0

@media screen and (min-width: 900px)
  section.events
    img
      border-radius: 2.6rem

    .content
      max-width: 51.6rem
      padding: 10rem 0

</style>
