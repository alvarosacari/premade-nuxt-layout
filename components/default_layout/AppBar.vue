<template>
  <v-app-bar
    dark
    color="primary"
    :clipped-left="value.clipped"
    fixed
    app
  >
    <v-app-bar-nav-icon @click.stop="value.drawer = !value.drawer" />
    <v-toolbar-title v-text="title" />
    <v-spacer />
  </v-app-bar>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      default () { return {} }
    },
    title: {
      type: String,
      default: ''
    }
  }
}
</script>
