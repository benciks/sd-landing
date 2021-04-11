<template>
  <div>
    <div class="hero">
      <div>
        <div class="text">
          <h3 class="order-1 bold">
            Školy
          </h3>
          <p class="copy-l">
            Saw them. Moveth abundantly don't sea us i greater. Don't one cattle their i tree is fruitful whales morting abundantly to Our.
          </p>
        </div>
        <img src="@/static/schools.svg" alt="School illustration">
      </div>
    </div>
    <div class="schools">
      <NuxtLink v-for="school in schools" :key="school.id" class="school" :to="'/schools/' + school.id">
        <Card :image="school.image" :title="school.title" :location="school.location" />
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
      schools: [
        {
          id: '1',
          title: 'Spsdtt',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          location: 'Trnava'
        },
        {
          id: '2',
          title: 'Spsdtt',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          location: 'Trnava'
        },
        {
          id: '2',
          title: 'Spsdtt',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          location: 'Trnava'
        },
        {
          id: '3',
          title: 'Spsdtt',
          image: 'https://images.unsplash.com/photo-1549455905-7692efd12860?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
          location: 'Trnava'
        }
      ]
    }
  }
})
</script>
<style scoped lang="sass">
.hero
  padding-top: 20.3rem
  background: $ui6

  div
    max-width: 90rem
    margin: 0 auto

    .text
      text-align: center
      display: flex
      flex-direction: column
      align-items: center
      margin-bottom: $xxl

      h3
        margin-bottom: $l

      p
        color: $ui2

    img
      padding: 0 $l
      width: 100%
      max-width: 90rem
      margin: 0 auto

.schools
  margin: 8rem auto 0 auto
  display: flex
  flex-direction: column
  align-items: center

  a
    width: 90%
    text-decoration: none
    margin-bottom: $l

@media screen and (min-width: 900px)
  .hero
    padding-bottom: 10.3rem

    div
      display: flex
      align-items: center
      justify-content: space-between

      .text
        text-align: left
        align-items: start

        p
          width: 44rem

      .image
        max-width: 40rem
        padding: 0

  .schools
    max-width: 90rem
    margin: 8rem auto 10rem auto
    display: grid
    grid-template-columns: repeat(3, auto)

    a
      width: 28.4rem

</style>
