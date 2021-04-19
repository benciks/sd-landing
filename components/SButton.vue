<template>
  <button :class="type" class="s-button">
    <span class="value copy-m bold">
      {{ value }}
    </span>
    <ArrowRightIcon v-if="type === 'textMore'" />
  </button>
</template>

<script>
import Vue from 'vue'
import { ArrowRightIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    ArrowRightIcon
  },
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
  display: flex
  align-items: center
  justify-content: center

  .value
    color: $white
    white-space: nowrap

  &:hover
    background: darken($primary, 5%)

  &.textMore
    background: none
    padding-left: 0

    .value
      color: $primary

    svg
      color: $primary
      height: 2.2rem
      width: 2.2rem
      margin-left: $xxs

  &.invert
    background: $white

    .value
      color: $primary

    &:hover
      background: darken($white, 3%)

@media screen and (max-width: 768px)
  button
    &.textMore
      padding: 0
      background: $ui5
      width: 100%
</style>
