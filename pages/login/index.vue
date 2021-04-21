<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="email" type="email" placeholder="Email" :model-value="email" :validation="validationMsg($v.email)" />
      <SInput v-model="password" type="password" placeholder="Heslo" :model-value="name" :validation="validationMsg($v.password)" />
      <p v-if="failed" class="error">
        Email alebo heslo je nesprávne
      </p>
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
import { required, email } from 'vuelidate/lib/validators'
import { validationMessage } from 'vuelidate-messages'

const formMessages = {
  required: () => 'Toto pole je povinné',
  email: () => 'Zadajte email v správnom formáte'
}

export default Vue.extend({
  layout: 'auth',
  middleware: 'guest',
  data () {
    return {
      email: '',
      password: '',
      failed: false
    }
  },
  validations: {
    email: { required, email },
    password: { required }
  },
  methods: {
    async onSubmit () {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        try {
          await this.$auth.loginWith('local', {
            data: {
              email: this.email,
              password: this.password
            }
          })
        } catch (e) {
          this.$router.push('/login')
          this.failed = true
        }

        this.$router.push('/admin')
      }
    },
    validationMsg: validationMessage(formMessages)
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

    .error
      color: $red

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
