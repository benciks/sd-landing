<template>
  <div class="container">
    <div class="head">
      <div class="title">
        <ArrowLeftIcon />
        <h3 class="order-3 bold">
          Pridať školu
        </h3>
      </div>
      <div class="actions">
        <SButton type="invert" value="Uložiť ako koncept" @click.native="saveConcept" />
        <SButton type="primary" value="Publikovať" @click.native="publish" />
      </div>
    </div>
    <div class="image-upload">
      <img v-if="imgUrl" :src="imgUrl" alt="">
      <div>
        <input v-if="!fileSelected" type="file" @change="inputChange">
        <SButton v-if="fileSelected" type="Primary" value="Nahrať fotku" @click.native="onUpload" />
      </div>
    </div>
    <div class="details">
      <div class="section-title">
        <BoxIcon />
        <p class="copy-m bold">
          Detaily
        </p>
      </div>
      <div class="inputs">
        <SInput v-model="school.name" placeholder="Meno školy" class="name" :model-value="school.name" />
        <SInput v-model="school.url" placeholder="Url" class="url" :model-value="school.url" />
        <SInput v-model="school.address" placeholder="Adresa" class="adress" :model-value="school.address" />
        <SInput v-model="school.postal" placeholder="PSČ" class="postal" :model-value="school.postal" />
        <SInput v-model="school.city" placeholder="Mesto" class="city" :model-value="school.city" />
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
      imgUrl: '',
      image: '',
      school: {},
      headers: {
        'Content-Type': 'application/octet-stream',
        Authorization: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiSm9obiBEb2UiLCJpYXQiOjE1MTYyMzkwMjIsInVwbG9hZGVySWQiOiJzaW1vbiIsInVwbG9hZGVyVHlwZSI6IlVTRVIiLCJleHAiOjE2Mjg0NDUzNjh9.AAMzQ1vSBrS_Afk3f1hMxmZaYyuTmbRFNIqzeWulHLA'
      }
    }
  },
  computed: {
    schoolUrl () {
      return '/schools/' + this.$route.params.id
    }
  },
  beforeMount () {
    this.fetchSchool()
  },
  methods: {
    composeSchool (schoolStatus) {
      return {
        name: this.school.name,
        url: this.school.url,
        address: this.school.address,
        postal: this.school.postal,
        city: this.school.city,
        img: '',
        status: schoolStatus
      }
    },
    async fetchSchool () {
      if (this.$route.params.id !== 'create') {
        this.school = await this.$axios.$get(this.schoolUrl)
      }
    },
    async saveConcept () {
      const school = this.composeSchool('unpublished')

      if (this.$route.params.id !== 'create') {
        await this.$axios.$patch(this.schoolUrl, school)
      } else {
        await this.$axios.$post('/schools', school)
      }
      await this.$router.push('/admin/schools')
    },
    async publish () {
      const school = this.composeSchool('published')

      if (this.$route.params.id !== 'create') {
        await this.$axios.$patch(this.schoolUrl, school)
      } else {
        await this.$axios.$post('/schools', school)
      }
      await this.$router.push('/admin/schools')
    },
    inputChange (event, image) {
      this.fileSelected = event.target.files[0]
      this.imgUrl = URL.createObjectURL(this.fileSelected)
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

    async onUpload () {
      const data = await this.getBase64(this.fileSelected)

      const blob = this.dataURItoBlob(data)

      const res = await this.$axios.post('https://file.dokedu.org/upload', blob, {
        headers: this.headers
      })
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

    svg
      margin-right: $xs

  .actions
    display: flex

    button
      margin-left: $m

.image-upload
  max-width: 68rem
  margin: $xl auto 0 auto
  height: 23.5rem
  display: flex
  align-items: center
  justify-content: center
  background: $white
  border-radius: 8px
  border: 1px solid $ui5
  position: relative

  img
    position: absolute
    height: 100%
    width: 100%
    object-fit: cover
    border-radius: 8px

  div
    z-index: 1

.details
  max-width: 68rem
  margin: $xl auto 0 auto

  .inputs
    display: flex
    flex-wrap: wrap
    justify-content: space-between

    .name
      width: 43.7rem
      margin-bottom: $m

    .url
      width: 22.5rem

    .adress
      width: 27.9rem

    .postal
      width: 14rem

    .city
      width: 22.5rem

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
