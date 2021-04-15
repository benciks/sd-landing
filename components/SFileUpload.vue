<template>
  <div class="c-file-upload">
    <input id="file" type="file" name="file" @change.prevent="$emit('change', $event)">
    <label for="file">Vybrať fotku</label>
  </div>
</template>

<style scoped lang="sass">
.c-file-upload

  input
    width: 0.1px
    height: 0.1px
    opacity: 0
    overflow: hidden
    position: absolute
    z-index: -1

  label
    height: 4.5rem
    @extend %copy-m
    @extend %bold
    background: $primary
    padding: $s $l
    border-radius: 8px
    cursor: pointer
    color: $white
    transition: 0.2s ease-in-out
    display: inline-block

    &:hover
      background: darken($primary, 5%)
</style>
