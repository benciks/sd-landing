<template>
  <div class="card">
    <div class="image">
      <img :src="image" alt="image">
    </div>
    <div class="details">
      <div class="copy-l bold title">
        {{ title }}
      </div>
      <div v-if="location" class="extra">
        <MapPinIcon />
        <div class="copy-s bold">
          {{ location }}
        </div>
      </div>
      <div v-if="date" class="extra">
        <CalendarIcon />
        <div class="copy-s">
          {{ date }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { MapPinIcon, CalendarIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    MapPinIcon,
    CalendarIcon
  },
  props: {
    image: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: 'Title'
    },
    location: {
      type: String,
      default: ''
    },
    date: {
      type: String,
      default: ''
    }
  }
})
</script>

<style scoped lang="sass">
.card
  width: 100%
  background: $ui6
  border-radius: 8px
  border: 1px solid $ui5

  .image
    height: 17.1rem
    width: 100%

    img
      height: 100%
      width: 100%
      object-fit: cover
      border-radius: 8px 8px 0 0

  .details
    padding: $s $m $m $m

    .title
      margin-bottom: $m

    .extra
      display: flex
      align-items: center

      svg
        height: 18px
        width: 18px
        color: $ui3

      div
        color: $ui3
        margin-left: $xxs
</style>
