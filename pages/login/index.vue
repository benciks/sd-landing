<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="email" type="email" placeholder="Email" class="input" />
      <SInput v-model="password" type="password" placeholder="Heslo" class="input" />
      <div class="buttons">
        <SButton value="Prihlásiť" @click.native="onSubmit" />
        <NuxtLink to="/login/forgot">
          <SButton value="Zabudli ste heslo?" type="invert" />
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  layout: 'auth',
  middleware: 'guest',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    async onSubmit () {
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/admin')
      } catch (e) {
        this.error = e.error.data.message
      }
    }
  }
})
</script>

<style scoped lang="sass">
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

    .input
      margin-bottom: $s

    .buttons
      margin-top: $l
      justify-content: space-between
      width: 100%

      a
        text-decoration: none

        button
          margin-top: $s

      .s-button::v-deep
        width: 100%

</style>
