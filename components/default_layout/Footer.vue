<template>
  <v-footer :fixed="fixed" app>
    <span>{{ text }}</span>
  </v-footer>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    fixed: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    text() {
      const copy = '©'
      const year = new Date().getFullYear()
      return `${copy} ${year}`
    }
  }
})
</script>

<style scoped></style>
