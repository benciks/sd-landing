<template>
  <div class="error-layout">
    <h1 v-if="error.statusCode === 404" class="order-2">
      Stránka nebola nájdená
    </h1>
    <h1 v-else class="order-2">
      Vyskytla sa chyba - {{ error.statusCode }}
    </h1>
    <NuxtLink to="/">
      <SButton value="Späť na domovskú stránku" />
    </NuxtLink>
  </div>
</template>

<script>
export default {
  layout: 'auth',
  props: {
    error: {
      type: Object,
      default: null
    }
  }
}
</script>

<style scoped lang="sass">
.error-layout
  height: 100vh
  display: flex
  align-items: center
  justify-content: center
  flex-direction: column

  h1
    margin-bottom: $xl

  a
    text-decoration: none

</style>
