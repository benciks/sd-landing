<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="email" type="email" placeholder="Email" :model-value="email" :validation="validationMsg($v.email)" />
      <SButton value="Odoslať" @click.native="onSubmit" />
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
  data () {
    return {
      email: ''
    }
  },
  validations: {
    email: { required, email }
  },
  methods: {
    async onSubmit () {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        await this.$axios.post('/login/forgot', {
          email: this.email
        })

        await this.$router.push('/')
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

    button
      margin-top: $l

</style>
