<template>
  <div v-if="active" v-on-clickaway="away" class="dropdown-content">
    <slot />
  </div>
</template>

<script>
import { mixin as clickaway } from 'vue-clickaway'

export default {
  mixins: [clickaway],
  inject: ['sharedState'],
  computed: {
    active () {
      return this.sharedState.active
    }
  },
  methods: {
    away () {
      this.sharedState.active = false
    }
  }
}
</script>

<style scoped lang="sass">
.dropdown-content
  background: $white
  border-radius: 8px
  position: absolute
  right: 0
  top: 3rem
  z-index: 3
  padding: $s $s $xxs $s
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.04), 0 0 2px rgba(0, 0, 0, 0.06), 0 0 1px rgba(0, 0, 0, 0.04)
</style>
