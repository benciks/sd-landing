<template>
  <div class="users">
    <div class="head">
      <h3 class="order-3 bold">
        Používatelia
      </h3>
      <div>
        <SInput v-model="searchQuery" type="Search" placeholder="Hľadajte používateľa" class="search" />
        <SDropdown>
          <template #toggler>
            <SButton value="Pozvať používateľa" />
          </template>
          <SDropdownContent>
            <div class="invite">
              <SInput v-model="inviteEmail" placeholder="Zadajte email" class="invite-input" />
              <SButton value="Pozvať" @click.native="inviteUser()" />
            </div>
          </SDropdownContent>
        </SDropdown>
      </div>
    </div>
    <div class="columns">
      <p class="label">
        Meno
      </p>
      <p class="label email">
        Email
      </p>
      <p class="label registred">
        Registrovaný
      </p>
      <p class="label role">
        Rola
      </p>
    </div>
    <div class="items">
      <div v-for="user in filteredUsers" :key="user.id" class="item">
        <p class="copy-m bold">
          {{ user.name }}
        </p>
        <p class="email copy-m">
          {{ user.email }}
        </p>
        <p class="registred copy-m">
          {{ normalizeDate(user.registredAt) }}
        </p>
        <div class="role">
          <p class="copy-s">
            Admin
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  layout: 'admin',
  middleware: 'auth',
  data () {
    return {
      searchQuery: '',
      inviteEmail: '',
      users: []
    }
  },
  computed: {
    filteredUsers () {
      if (this.searchQuery) {
        return this.users.filter((item) => {
          return item.name.startsWith(this.searchQuery) || item.email.startsWith(this.searchQuery)
        })
      } else {
        return this.users
      }
    }
  },
  beforeMount () {
    this.fetchUsers()
  },
  methods: {
    async fetchUsers () {
      this.users = await this.$axios.$get('/users')
    },
    normalizeDate (date) {
      const normalDate = new Date(date)
      return normalDate.getDay() + '.' + normalDate.getMonth() + '.' + normalDate.getFullYear()
    },
    async inviteUser () {
      const invite = {
        email: this.inviteEmail
      }

      await this.$axios.$post('/inviteUser', invite)
    }
  }
})
</script>

<style scoped lang="sass">
.users
  .head
    display: flex
    justify-content: space-between
    align-items: center
    margin-top: $xxl
    position: relative

    div
      display: flex

      .search
        width: 32rem
        margin-right: $s

      div
        ::v-deep .dropdown-content
          top: 5.6rem
          padding-bottom: $s

      .invite
        display: flex

        button
          margin-left: $s

        .invite-input
          width: 25rem

  .items

    .item
      background: $white
      border: 1px solid $ui5
      border-bottom: 0
      padding: $m $l
      display: flex
      align-items: center
      position: relative

      .email
        position: absolute
        left: 257px

      .registred
        position: absolute
        left: 538px

      .role
        position: absolute
        left: 760px
        padding: $xxs $s
        background: $primary
        border-radius: 99em

        p
          color: $white

    .item:first-of-type
      border-radius: 8px 8px 0 0

    .item:last-of-type
      border-radius: 0 0 8px 8px
      border-bottom: 1px solid $ui5

  .columns
    display: flex
    padding-left: $l
    padding-bottom: $xs
    align-items: center
    position: relative
    margin-top: $xxl

    .email
      position: absolute
      left: 257px

    .registred
      position: absolute
      left: 538px

    .role
      position: absolute
      left: 760px

    p
      color: $ui4

</style>
