<template>
  <div v-on-clickaway="away" @click="toggle">
    <slot name="toggler">
      <button>Toggle</button>
    </slot>
    <slot />
  </div>
</template>

<script>
import Vue from 'vue'
import { mixin as clickaway } from 'vue-clickaway'

export default Vue.extend({
  mixins: [clickaway],
  provide () {
    return {
      sharedState: this.sharedState
    }
  },
  data () {
    return {
      sharedState: {
        active: false
      }
    }
  },
  methods: {
    toggle () {
      this.sharedState.active = !this.sharedState.active
    },
    away () {
      this.sharedState.active = false
    }
  }
})
</script>
