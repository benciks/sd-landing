<template>
  <header :class="{ sticky }">
    <div class="header-container">
      <NuxtLink to="/">
        <Logo />
      </NuxtLink>
      <nav>
        <div class="links">
          <NuxtLink v-for="(link, index) in links" :key="index" :to="link.to" class="bold">
            {{ link.name }}
          </NuxtLink>
        </div>
        <div class="actions">
          <div class="menu-toggle" @click="openMobileMenu">
            <MenuIcon />
          </div>
        </div>
      </nav>
    </div>
    <div class="mobile-nav" :class="{ active: mobileMenuOpen }">
      <nav>
        <div class="close" @click="closeMobileMenu">
          <XIcon />
        </div>
        <div class="links">
          <NuxtLink
            v-for="(link, index) in links"
            :key="index"
            :to="link.to"
            @click.native="handleNavigation"
          >
            {{ link.name }}
          </NuxtLink>
        </div>
      </nav>
    </div>
  </header>
</template>

<script lang="js">
import Vue from 'vue'
import { XIcon, MenuIcon } from 'vue-feather-icons'
import { mapGetters } from 'vuex'

export default Vue.extend({
  components: {
    XIcon,
    MenuIcon
  },
  data () {
    return {
      links: [
        { name: 'Domov', to: '/' },
        { name: 'Podujatia', to: '/events' },
        { name: 'Školy', to: '/schools' },
        { name: 'Články', to: '/articles' }
      ],
      wScroll: 0,
      sticky: false,
      mobileMenuOpen: false,
      loggedIn: this.$auth.loggedIn
    }
  },
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  beforeMount () {
    window.addEventListener('scroll', this.handleScroll)
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy () {
    window.removeEventListener('scroll', this.handleScroll)
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    openMobileMenu () {
      this.mobileMenuOpen = true
    },
    closeMobileMenu () {
      this.mobileMenuOpen = false
    },
    handleResize () {
      this.mobileMenuOpen = false
    },
    handleNavigation () {
      this.closeMobileMenu()
    },
    handleScroll () {
      this.wScroll = window.scrollY
      if (this.wScroll > 50) {
        this.sticky = true
      } else {
        this.sticky = false
      }
    },
    async logout () {
      await this.$auth.logout()
    }
  }
})
</script>

<style scoped lang="sass">
header
  z-index: 100
  position: fixed
  width: 100%
  transition: all 300ms ease
  background: none
  &.sticky
    background: white
    padding-top: 0px
    box-shadow: $small-shadow
  .header-container
    width: 100%
    padding: $l 0
    display: flex
    align-items: center
    justify-content: space-between

    nav
      display: flex
      align-items: center
      .actions
        display: flex
        align-items: center
      a + a
        margin-left: $xxl
  nav
    margin: 0
    a
      @extend %copy-m
      color: $ui3
      text-decoration: none
      font-weight: normal
      font-size: 16px
      line-height: 16px
      &.nuxt-link-exact-active
        font-weight: bold
        color: $ui1
      &.home.nuxt-link-exact-active.nuxt-link-active
        font-weight: bold
  .mobile-nav
    position: fixed
    background: white
    width: 100%
    height: 100%
    top: 0
    left: 100%
    padding: 100px 40px 60px 40px
    transition: 200ms ease-in-out

    a
      font-size: 24px
    &.active
      left: 0%
    .close
      position: absolute
      top: 60px
      right: 24px
      width: 48px
      height: 48px
      display: flex
      align-items: center
      justify-content: center
      z-index: 10

      svg
        color: $ui3
    nav
      display: flex
      height: 100%
      flex-direction: column
      justify-content: space-between
      a
        display: block
        padding: $l

  .user
    display: flex
    align-items: center
    margin-left: $xl

    svg
      cursor: pointer
      color: $ui3
      transition: .2s ease-in-out
      margin-left: $m

      &:hover
        color: $ui1

@media screen and (max-width: 700px)
  header
    .header-container
      padding: $l $xl
      nav
        .links, .actions .login
          display: none
        a + a
          margin-left: $s
        a
          padding: 10px
        .menu-toggle
          margin-left: $s

          svg
            color: $ui1

@media screen and (max-width: 1030px)
  header
    .header-container
      padding: $l $xl

@media screen and (min-width: 700px)
  header
    display: flex
    justify-content: center
    padding-top: 56px
    .menu-toggle
      display: none
    .header-container
      max-width: 1000px
      nav
        .actions
          margin-left: $xl
          a + a
            margin-left: $l
</style>
