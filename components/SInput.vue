<template>
  <input :type="type" :placeholder="placeholder" class="copy-m">
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  props: {
    type: {
      type: String,
      default: 'text'
    },
    placeholder: {
      type: String,
      default: 'value'
    }
  }
})
</script>

<style scoped lang="sass">
input
  height: 4.5rem
  width: 100%
  border: 1px solid $ui5
  border-radius: 8px
  padding-left: $s
  transition: .2s ease-in-out

  &:hover
    border: 1px solid $ui4

  &:active, &:focus
    border: 1px solid $primary

  &::placeholder
    color: $ui4

</style>
