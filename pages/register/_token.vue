<template>
  <div class="container">
    <div class="form">
      <Logo class="logo" />
      <SInput v-model="email" type="email" placeholder="Email" :model-value="email" :validation="validationMsg($v.email)" />
      <SInput v-model="name" type="text" placeholder="Celé meno" :model-value="name" :validation="validationMsg($v.name)" />
      <SInput v-model="password" type="password" placeholder="Heslo" :model-value="password" :validation="validationMsg($v.password)" />
      <SInput v-model="repeatPassword" type="password" placeholder="Heslo" :model-value="repeatPassword" :validation="validationMsg($v.repeatPassword)" />
      <SButton value="Registrovať" @click.native="onSubmit" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import { validationMessage } from 'vuelidate-messages'

const formMessages = {
  required: () => 'Toto pole je povinné',
  minLength: ({ $params }) => `Heslo musí byť dlhé aspoň ${$params.minLength.min} znakov.`,
  email: () => 'Zadajte email v správnom formáte',
  sameAsPassword: () => 'Heslá by sa mali zhodovať'
}

export default Vue.extend({
  layout: 'auth',
  data () {
    return {
      name: '',
      email: '',
      password: '',
      repeatPassword: ''
    }
  },
  validations: {
    name: { required },
    email: { required, email },
    password: { required, minLength: minLength(8) },
    repeatPassword: {
      sameAsPassword: sameAs('password')
    }
  },
  methods: {
    async onSubmit () {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        await this.$axios.post('/registration', {
          token: this.$route.params.token,
          name: this.name,
          email: this.email,
          password: this.password,
          img: ''
        })
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        await this.$router.push('/admin')
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
  overflow: hidden

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
