<template>
  <div class="container">
    <div class="head">
      <div class="title">
        <NuxtLink to="/admin">
          <ArrowLeftIcon />
        </NuxtLink>
        <h3 class="order-3 bold">
          Nastavenia profilu
        </h3>
      </div>
      <div class="actions">
        <SButton type="primary" value="Uložiť zmeny" @click.native="publish" />
      </div>
    </div>
    <div class="image-upload">
      <div class="image">
        <img v-if="imgUrl" :src="imgUrl" alt="Profile picture">
      </div>
      <SFileUpload class="button" @change="inputChange" />
      <SButton v-if="tempImg" type="invert" class="button" value="Nahrať" @click.native="onUpload" />
    </div>
    <div class="details">
      <div class="section-title">
        <BoxIcon />
        <p class="copy-m bold">
          Detaily
        </p>
      </div>
      <div class="inputs">
        <SInput v-model="user.name" placeholder="Celé meno" class="name" :model-value="user.name" />
        <SInput v-model="user.email" placeholder="Email" class="email" :model-value="user.email" />
        <SInput v-model="password" type="password" placeholder="Heslo" class="password" :model-value="password" />
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { ArrowLeftIcon, BoxIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    ArrowLeftIcon,
    BoxIcon
  },
  layout: 'auth',
  middleware: 'auth',
  data () {
    return {
      fileSelected: false,
      tempImg: '',
      password: '',
      user: {},
      headers: {
        'Content-Type': 'application/octet-stream',
        Authorization: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiSm9obiBEb2UiLCJpYXQiOjE1MTYyMzkwMjIsInVwbG9hZGVySWQiOiJzaW1vbiIsInVwbG9hZGVyVHlwZSI6IlVTRVIiLCJleHAiOjE2Mjg0NDUzNjh9.AAMzQ1vSBrS_Afk3f1hMxmZaYyuTmbRFNIqzeWulHLA'
      }
    }
  },
  computed: {
    imgUrl () {
      if (this.tempImg) {
        return this.tempImg
      } else {
        return this.user.img
      }
    }
  },
  beforeMount () {
    this.fetchUser()
  },
  methods: {
    async fetchUser () {
      this.user = await this.$axios.$get('/users/me')
    },
    inputChange (event, image) {
      this.fileSelected = event.target.files[0]
      this.tempImg = URL.createObjectURL(this.fileSelected)
    },
    dataURItoBlob (dataURI) {
      // convert base64 to raw binary data held in a string
      // doesn't handle URLEncoded DataURIs - see SO answer #6850276 for code that does this
      const byteString = atob(dataURI.split(',')[1])

      // separate out the mime component
      const mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0]

      // write the bytes of the string to an ArrayBuffer
      const ab = new ArrayBuffer(byteString.length)

      // create a view into the buffer
      const ia = new Uint8Array(ab)

      // set the bytes of the buffer to the correct values
      for (let i = 0; i < byteString.length; i++) {
        ia[i] = byteString.charCodeAt(i)
      }

      // write the ArrayBuffer to a blob, and you're done
      return new Blob([ab], { type: mimeString })
    },
    getBase64 (file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader()
        reader.readAsDataURL(file)
        reader.onload = () => resolve(reader.result)
        reader.onerror = error => reject(error)
      })
    },
    async publish () {
      const user = {
        name: this.user.name,
        email: this.user.email
      }
      if (this.tempImg) { user.img = this.tempImg }
      if (this.password) { user.password = this.password }

      const res = await this.$axios.patch('/users/me', user)

      if (res.status === 200) {
        await this.$router.push('/admin')
      }
    },
    async onUpload () {
      const data = await this.getBase64(this.fileSelected)
      const blob = this.dataURItoBlob(data)

      const res = await this.$axios.post('https://file.dokedu.org/upload', blob, {
        headers: this.headers
      })

      if (res.status === 200) {
        this.tempImg = 'https://file.dokedu.org/file/' + res.data.id
      }
    }
  }
})
</script>

<style scoped lang="sass">
.container
  height: 100vh
  width: 100%

.head
  width: 68rem
  display: flex
  padding-top: $xxl
  margin: 0 auto
  justify-content: space-between
  align-items: center

  .title
    display: flex

    a
      height: 24px
      width: 24px
      margin-right: $xs

      svg
        color: $ui1
        transition: .2s ease-in-out

        &.hover
          color: $ui2

.image-upload
  max-width: 68rem
  margin: $xl auto 0 auto
  display: flex
  align-items: center

  .image
    width: 8rem
    height: 8rem
    border-radius: 99em
    border: 1px solid $ui5
    background: $white

    img
      height: 100%
      width: 100%
      object-fit: cover
      border-radius: 99em

  .button
    margin-left: $l

.details
  max-width: 68rem
  margin: $xl auto 0 auto

  .inputs
    display: flex
    flex-wrap: wrap
    justify-content: space-between

    .name
      width: 33.3rem
      margin-bottom: $m

    .email
      width: 33.3rem

    .password
      width: 33.3rem

.section-title
  display: flex
  align-items: center
  margin-bottom: $m

  svg
    height: 18px
    width: 18px
    color: $ui3
    margin-right: $xxs

  p
    color: $ui3
</style>
