<template>
  <button>
    <span class="value copy-m bold">
      {{ value }}
    </span>
  </button>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  props: {
    value: {
      type: String,
      required: true
    },
    type: {
      type: String,
      default: 'primary'
    }
  }
})
</script>

<style scoped lang="sass">
button
  height: 4.5rem
  padding: 0 $l
  border: 0
  border-radius: 8px
  background: $primary
  cursor: pointer
  transition: .2s ease-in-out

  .value
    color: $white

  &:hover
    background: darken($primary, 5%)
</style>
