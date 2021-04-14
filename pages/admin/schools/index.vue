<template>
  <div class="schools">
    <div class="head">
      <h3 class="order-3 bold">
        Školy
      </h3>
      <div>
        <SInput type="Search" placeholder="Hľadajte školu" class="search" />
        <NuxtLink to="/admin/schools/create">
          <SButton value="Pridať školu" to="/admin/schools/create" />
        </NuxtLink>
      </div>
    </div>
    <div class="columns">
      <p class="label">
        Názov
      </p>
      <p class="label address">
        Adresa
      </p>
      <p class="label url">
        Url
      </p>
      <p class="label status">
        Status
      </p>
    </div>
    <div class="items">
      <div v-for="school in schools" :key="school.url" class="item">
        <p class="copy-m bold">
          {{ school.name }}
        </p>
        <p class="address copy-m">
          {{ school.address }}, {{ school.city }}
        </p>
        <p class="url copy-m">
          {{ school.url }}
        </p>
        <div v-if="school.status === 'published'" class="status published">
          <p class="copy-s">
            Publikované
          </p>
        </div>
        <div v-if="school.status === 'unpublished'" class="status unpublished">
          <p class="copy-s">
            Nepublikované
          </p>
        </div>
        <NuxtLink :to="'/admin/schools/' + school.id" class="more">
          <MoreVerticalIcon />
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { MoreVerticalIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    MoreVerticalIcon
  },
  layout: 'admin',
  middleware: 'auth',
  data () {
    return {
      schools: []
    }
  },
  beforeMount () {
    this.fetchSchools()
  },
  methods: {
    async fetchSchools () {
      this.schools = await this.$axios.$get('/schools')
    }
  }
})
</script>

<style scoped lang="sass">
.schools
  .head
    display: flex
    justify-content: space-between
    align-items: center
    margin-top: $xxl

    div
      display: flex

      a
        text-decoration: none

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

      .address
        position: absolute
        left: 367px

      .url
        position: absolute
        left: 572px

      .status
        padding: $xxs $s
        position: absolute
        left: 729px
        border-radius: 99em

      .published
        background: $green

        p
          color: $white

      .unpublished
        background: $ui5

      .more
        position: absolute
        right: $l
        display: flex
        align-items: center

        svg
          color: $ui4
          height: 18px
          width: 18px

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

    .address
      position: absolute
      left: 367px

    .url
      position: absolute
      left: 572px

    .status
      position: absolute
      left: 729px

    p
      color: $ui4

</style>
