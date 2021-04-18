<template>
  <div class="container">
    <NavAdmin />
    <div class="content">
      <div class="actions">
        <div class="active">
          <BoxIcon />
          <p class="copy-m bold">
            {{ route }}
          </p>
        </div>
        <div class="user">
          <SDropdown>
            <template #toggler>
              <div class="toggle">
                <img :src="loggedInUser.img" alt="">
                <p class="copy-m bold">
                  {{ loggedInUser.name }}
                </p>
                <ChevronDownIcon />
              </div>
            </template>
            <SDropdownContent>
              <NuxtLink to="/admin/profile/" class="link">
                <UserIcon />
                <div class="copy-m">
                  Upraviť profil
                </div>
              </NuxtLink>
              <div class="link" @click="logout()">
                <LogOutIcon />
                <div class="copy-m">
                  Odhlásiť sa
                </div>
              </div>
            </SDropdownContent>
          </SDropdown>
        </div>
      </div>
      <Nuxt />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { mapGetters } from 'vuex'
import { LogOutIcon, BoxIcon, ChevronDownIcon, UserIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    LogOutIcon,
    BoxIcon,
    ChevronDownIcon,
    UserIcon
  },
  computed: {
    ...mapGetters(['loggedInUser']),
    route () {
      switch (this.$route.name) {
        case 'admin':
          return 'Domov'
        case 'admin-schools':
          return 'Školy'
        case 'admin-articles':
          return 'Články'
        case 'admin-users':
          return 'Používatelia'
      }
      return undefined
    }
  },
  methods: {
    async logout () {
      await this.$auth.logout()
    }
  }
})
</script>

<style scoped lang="sass">
.container
  display: flex
  background: $ui6

  .content
    margin: 0 auto

  .actions
    display: flex
    justify-content: space-between
    width: 90rem
    margin-top: $xxl

    p
      color: $ui3

    .active
      display: flex
      align-items: center

      svg
        width: 20px
        height: 20px
        color: $ui3
        margin-right: $xs

    .user
      position: relative

      .toggle
        display: flex
        align-items: center
        cursor: pointer

        img
          border-radius: 99em
          height: 2.4rem
          width: 2.4rem
          object-fit: cover
          margin-right: $xs

        p, svg
          transition: 0.2s ease-in-out

        svg
          margin-left: $s

        &:hover
          p, svg
            color: $ui1

      svg
        width: 20px
        height: 20px
        color: $ui3
        cursor: pointer

      .link
        text-decoration: none
        display: flex
        padding: $xs $l $xs $s
        width: auto
        white-space: nowrap
        align-items: center
        border: 1px solid $white
        border-radius: 8px
        transition: 0.2s ease-in-out
        margin-bottom: $xs
        cursor: pointer

        &:hover
          background: $ui6
          border: 1px solid $ui5

          div, svg
            color: $primary

        div
          margin-left: $s
          @extend %bold
          color: $ui2
          transition: 0.2s ease-in-out

        svg
          color: $ui2
          transition: 0.2s ease-in-out
</style>
