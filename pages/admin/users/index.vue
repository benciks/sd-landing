<template>
  <div class="users">
    <div class="head">
      <h3 class="order-3 bold">
        Používatelia
      </h3>
      <div>
        <SInput type="Search" placeholder="Hľadajte používateľa" class="search" />
        <SButton value="Pozvať používateľa" />
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
      <div v-for="user in users" :key="user.id" class="item">
        <p class="copy-m bold">
          {{ user.name }}
        </p>
        <p class="email copy-m">
          {{ user.email }}
        </p>
        <p class="registred copy-m">
          {{ user.registred }}
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
      users: [
        {
          id: '1',
          name: 'John Doe',
          email: 'john.doe@gmail.com',
          registred: '13.2.2013'
        },
        {
          id: '2',
          name: 'John Doe',
          email: 'john.doe@gmail.com',
          registred: '13.2.2013'
        },
        {
          id: '3',
          name: 'John Doe',
          email: 'john.doe@gmail.com',
          registred: '13.2.2013'
        }
      ]
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

    div
      display: flex

      .search
        width: 32rem
        margin-right: $s

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
        left: 729px
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
      left: 729px

    p
      color: $ui4

</style>
