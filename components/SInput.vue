<template>
  <div class="input-container">
    <div class="input">
      <SearchIcon v-if="type === 'search'" />
      <input
        :type="type"
        :placeholder="placeholder"
        :value="modelValue"
        class="copy-m"
        @input="updateValue($event.target.value)"
      >
    </div>
    <div v-if="validation" class="error-container">
      <p class="error copy-m">
        {{ validation }}
      </p>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { SearchIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    SearchIcon
  },
  props: {
    type: {
      type: String,
      default: 'text'
    },
    placeholder: {
      type: String,
      default: 'value'
    },
    modelValue: {
      type: String,
      default: ''
    },
    validation: {
      type: String,
      default: ''
    }
  },
  methods: {
    updateValue (value) {
      this.$emit('input', value)
    }
  }
})
</script>

<style scoped lang="sass">
.input-container
  width: 100%

.input
  height: 4.5rem
  width: 100%
  border: 1px solid $ui5
  background: $white
  border-radius: 8px
  padding-left: $s
  transition: .2s ease-in-out
  display: flex
  align-items: center

  &:hover
    border: 1px solid $ui4

  &:active, &:focus
    border: 1px solid $primary

  &::placeholder
    color: $ui4

  input
    border: none
    outline: none
    background: none
    width: 100%
    height: 100%

  svg
    height: 18px
    width: 18px
    color: $ui4
    margin-right: $xs

.error-container
  padding-left: $s

  p
    color: $red
</style>
