<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="email" type="email" placeholder="Email" />
      <SButton value="Odoslať" @click.native="onSubmit" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  layout: 'auth',
  data () {
    return {
      email: ''
    }
  },
  methods: {
    async onSubmit () {
      try {
        await this.$axios.post('/login/forgot', {
          email: this.email
        })

        await this.$router.push('/')
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

    div
      margin-bottom: $s

    button
      margin-top: $l

</style>
