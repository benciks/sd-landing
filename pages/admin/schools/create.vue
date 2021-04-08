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
    <div class="details">
      <div class="section-title">
        <BoxIcon />
        <p class="copy-m bold">
          Detaily
        </p>
      </div>
      <div class="inputs">
        <SInput placeholder="Meno školy" class="name" />
        <SInput placeholder="Url" class="url" />
        <SInput placeholder="Adresa" class="adress" />
        <SInput placeholder="PSČ" class="postal" />
        <SInput placeholder="Mesto" class="city" />
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
  middleware: 'auth'
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
