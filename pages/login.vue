<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="user.email" type="email" placeholder="Email" />
      <SInput v-model="user.password" type="password" placeholder="Heslo" />
      <SButton value="Prihlásiť" @click.native="onSubmit" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  layout: 'auth',
  data () {
    return {
      user: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    onSubmit () {
      alert('hello')
    }
  }
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
