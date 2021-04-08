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
        <SButton type="invert" value="Uložiť ako koncept" />
        <SButton type="primary" value="Publikovať" />
      </div>
    </div>
    <div class="image-upload">
      <SButton type="Primary" value="Nahrať fotku" />
    </div>
    <div class="editor">
      <div class="section-title">
        <EditIcon />
        <p class="copy-m bold">
          Editor
        </p>
      </div>
      <client-only>
        <Tiptap />
      </client-only>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { ArrowLeftIcon, EditIcon } from 'vue-feather-icons'

export default Vue.extend({
  components: {
    ArrowLeftIcon,
    EditIcon
  },
  layout: 'auth',
  // middleware: 'auth',
  data () {
    return {
      id: '1',
      title: 'Zameranie odborov',
      url: 'zameranie-odborov',
      editedAt: '92601',
      author: '',
      content: ''
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
