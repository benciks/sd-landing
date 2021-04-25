<template>
  <div class="container">
    <div class="head">
      <div class="title">
        <input v-model="article.name" type="text" class="order-3 bold" placeholder="Zadajte názov stránky">
        <div class="url copy-m">
          /clanky/ <input v-model="article.url" :model-value="article.url" type="text" class="copy-m bold">
        </div>
      </div>
      <div class="actions">
        <SButton type="invert" value="Uložiť ako koncept" @click.native="saveConcept" />
        <SButton type="primary" value="Publikovať" @click.native="publish" />
      </div>
    </div>
    <div class="image-upload">
      <img v-if="imgUrl" :src="imgUrl" alt="">
      <div>
        <SFileUpload @change="inputChange" />
        <SButton v-if="tempImg" type="invert" value="Nahrať" @click.native="onUpload" />
      </div>
    </div>
    <div class="editor">
      <div class="section-title">
        <EditIcon />
        <p class="copy-m bold">
          Editor
        </p>
      </div>
      <client-only>
        <Tiptap v-model="article.content" />
      </client-only>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { EditIcon } from 'vue-feather-icons'
import { mapGetters } from 'vuex'
import { required } from 'vuelidate/lib/validators'

export default Vue.extend({
  components: {
    EditIcon
  },
  layout: 'auth',
  middleware: 'auth',
  data () {
    return {
      fileSelected: false,
      tempImg: '',
      article: {},
      headers: {
        'Content-Type': 'application/octet-stream',
        Authorization: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiSm9obiBEb2UiLCJpYXQiOjE1MTYyMzkwMjIsInVwbG9hZGVySWQiOiJzaW1vbiIsInVwbG9hZGVyVHlwZSI6IlVTRVIiLCJleHAiOjE2Mjg0NDUzNjh9.AAMzQ1vSBrS_Afk3f1hMxmZaYyuTmbRFNIqzeWulHLA'
      }
    }
  },
  validations: {
    article: {
      name: { required },
      url: { required }
    }
  },
  computed: {
    ...mapGetters(['loggedInUser']),
    articleUrl () {
      return '/articles/' + this.$route.params.url
    },
    imgUrl () {
      if (this.tempImg) {
        return this.tempImg
      } else {
        return this.article.img
      }
    }
  },
  beforeMount () {
    this.fetchArticle()
  },
  methods: {
    composeArticle (articleStatus) {
      return {
        name: this.article.name,
        url: this.article.url,
        author: this.loggedInUser.name,
        content: this.article.content,
        status: articleStatus
      }
    },
    async fetchArticle () {
      if (this.$route.params.url !== 'create') {
        this.article = await this.$axios.$get(this.articleUrl)
      }
    },
    async saveConcept () {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        const article = this.composeArticle('unpublished')
        if (this.tempImg) {
          article.img = this.tempImg
        } else if (this.article.img) {
          return
        } else {
          article.img = ''
        }

        if (!article.content) { article.content = '' }

        if (this.$route.params.url !== 'create') {
          await this.$axios.$patch(this.articleUrl, article)
        } else {
          await this.$axios.$post('/articles', article)
        }
        await this.$router.push('/admin/articles')
      }
    },
    async publish () {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        const article = this.composeArticle('published')
        if (this.tempImg) {
          article.img = this.tempImg
        } else if (this.article.img) {
          return
        } else {
          article.img = ''
        }

        if (!article.content) { article.content = '' }

        if (this.$route.params.url !== 'create') {
          await this.$axios.$patch(this.articleUrl, article)
        } else {
          await this.$axios.$post('/articles', article)
        }
        await this.$router.push('/admin/articles')
      }
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
    div
      display: flex
      color: $ui2

      input
        color: $ui2

    input
      border: none
      outline: none
      background: none
      color: $ui1

      &::placeholder
        color: $ui4

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
    display: flex

    button
      margin-left: $m

.editor
  max-width: 68rem
  margin: $xl auto 0 auto

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
