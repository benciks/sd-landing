<template>
  <nav>
    <Logo class="logo" />
    <div class="links">
      <NuxtLink to="/admin">
        <HomeIcon />
        <p class="copy-m bold">
          Domov
        </p>
      </NuxtLink>
      <NuxtLink to="/admin/schools">
        <BookIcon />
        <p class="copy-m bold">
          Školy
        </p>
      </NuxtLink>
      <NuxtLink to="/admin/articles">
        <PaperclipIcon />
        <p class="copy-m bold">
          Články
        </p>
      </NuxtLink>
      <NuxtLink to="/admin/users">
        <UsersIcon />
        <p class="copy-m bold">
          Používatelia
        </p>
      </NuxtLink>
    </div>
  </nav>
</template>

<script>
import Vue from 'vue'
import { HomeIcon, BookIcon, PaperclipIcon, UsersIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    HomeIcon,
    BookIcon,
    PaperclipIcon,
    UsersIcon
  }
})
</script>
<style scoped lang="sass">
nav
  height: 100vh
  width: 29rem
  background: $ui1
  display: flex
  flex-direction: column
  align-items: center

  .logo
    width: 124px
    height: auto
    margin-top: $xxl

  .links
    width: 83%
    margin-top: $xxl

    a
      display: flex
      align-items: center
      text-decoration: none
      color: $ui4
      height: 4rem
      margin-bottom: $m
      width: 100%
      padding-left: $s
      border-radius: 5px

      &.nuxt-link-exact-active.nuxt-link-active
        background: $ui2

        p, svg
          color: $white

      p
        color: $ui4
        margin-left: $xs

      svg
        height: 16px
        width: 16px

</style>
