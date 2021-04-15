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
        <SDropdown class="more">
          <template #toggler>
            <MoreVerticalIcon />
          </template>
          <SDropdownContent>
            <NuxtLink :to="'/admin/schools/' + school.id" class="link">
              <EditIcon />
              <div class="copy-m">
                Upraviť školu
              </div>
            </NuxtLink>
            <div class="link" @click="deleteSchool(school.id)">
              <DeleteIcon />
              <div class="copy-m">
                Zmazať školu
              </div>
            </div>
          </SDropdownContent>
        </SDropdown>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { MoreVerticalIcon, EditIcon, DeleteIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    MoreVerticalIcon,
    EditIcon,
    DeleteIcon
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
    },
    async deleteSchool (schoolId) {
      const url = '/schools/' + schoolId
      await this.$axios.$delete(url)
      await this.fetchSchools()
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
        left: 420px

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
        height: 18px

        svg
          color: $ui4
          height: 18px
          width: 18px
          cursor: pointer
          transition: 0.2s ease-in-out

          &:hover
            color: $ui1

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
      left: 420px

    .status
      position: absolute
      left: 729px

    p
      color: $ui4

</style>
