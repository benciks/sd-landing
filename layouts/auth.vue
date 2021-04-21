<template>
  <div>
    <LoadingScreen v-show="showHideSpinner" />
    <Nuxt />
  </div>
</template>

<script>
export default {
  data () {
    return {
      showHideSpinner: true
    }
  },
  beforeCreate () {
    this.showHideSpinner = true
  },
  mounted () {
    setTimeout(() => {
      this.showHideSpinner = false
    }, 350)
  }
}
</script>

<style scoped lang="sass">
*
  background: $ui6
</style>
