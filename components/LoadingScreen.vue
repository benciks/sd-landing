<template>
  <div class="splash-screen">
    <div class="spinner-wrapper">
      <div class="spinner" />
    </div>
  </div>
</template>

<style scoped lang="sass">
.splash-screen
  background: $ui6
  width: 100%
  height: 100%
  position: fixed
  z-index: 50
  box-sizing: border-box
  overflow: hidden

.spinner-wrapper
  position: absolute
  left: 50%
  top: 50%

  transform: translate(-50%, -50%)

.spinner
  width: 80px
  height: 80px
  margin: 100px auto
  background-color: $primary

  border-radius: 100%
  -webkit-animation: sk-scaleout 1s infinite ease-in-out
  animation: sk-scaleout 1s infinite ease-in-out

@-webkit-keyframes sk-scaleout
  0%
    -webkit-transform: scale(0)
  100%
    -webkit-transform: scale(1)
    opacity: 0

@keyframes sk-scaleout
  0%
    -webkit-transform: scale(0)
    transform: scale(0)
  100%
    -webkit-transform: scale(1)
    transform: scale(1)
    opacity: 0
</style>
