<template>
  <div>
    Admin or something
    {{ $auth.user.email }}
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  middleware: 'auth'
})
</script>
