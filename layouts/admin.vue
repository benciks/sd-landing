<template>
  <div class="container">
    <NavAdmin />
    <div class="subnav">
      <div class="actions">
        <div class="active">
          <BoxIcon />
          <p class="copy-m bold">
            {{ $route.name }}
          </p>
        </div>
        <div class="user">
          <p class="copy-m bold">
            {{ loggedInUser.name }}
          </p>
          <LogOutIcon @click="logout()" />
        </div>
      </div>
      <Nuxt />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { mapGetters } from 'vuex'
import { LogOutIcon, BoxIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    LogOutIcon,
    BoxIcon
  },
  computed: {
    ...mapGetters(['loggedInUser'])
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

  .subnav
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
      display: flex
      align-items: center

      svg
        width: 20px
        height: 20px
        color: $ui3
        margin-left: $s
        cursor: pointer
</style>
