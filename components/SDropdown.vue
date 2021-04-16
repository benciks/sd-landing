<template>
  <div class="s-dropdown">
    <div @click="toggle">
      <slot name="toggler">
        <button>Toggle</button>
      </slot>
    </div>
    <slot />
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
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
    }
  }
})
</script>
