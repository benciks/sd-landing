<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput type="email" placeholder="Email" />
      <SInput type="text" placeholder="Celé meno" />
      <SInput type="password" placeholder="Heslo" />
      <SInput type="password" placeholder="Zopakujte heslo" />
      <SButton value="Log in" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  layout: 'auth'
})
</script>

<style lang="sass">
.container
  height: 100vh
  display: flex
  align-items: center
  justify-content: center

  .form
    display: flex
    flex-direction: column
    align-items: center
    width: 28rem

    .logo
      height: auto
      width: 12.4rem
      margin-bottom: $xl

    input
      margin-bottom: $s

    button
      margin-top: $l

</style>
