<template>
  <footer>
    <div class="container">
      <Logo />
      <div class="links">
        <NuxtLink v-for="(link, index) in links" :key="index" :to="link.to" class="bold">
          {{ link.name }}
        </NuxtLink>
      </div>
      <p class="copy-m">
        Vytvoril Šimon Benčík pre Ministerstvo dopravy Slovenskej republiky
      </p>
    </div>
  </footer>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      links: [
        { name: 'Domov', to: '/' },
        { name: 'Podujatia', to: '/events' },
        { name: 'Školy', to: '/schools' },
        { name: 'Články', to: '/articles' }
      ]
    }
  }
})
</script>

<style scoped lang="sass">
footer
  width: 100%
  padding: 12rem 0 8rem 0

  .container
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center

    .links
      margin: $xl 0 $l 0

    a
      padding-left: $xl
      text-decoration: none
      color: $ui1

    a:first-of-type
      padding-left: 0

    p
      color: $ui3
      text-align: center

</style>
