<template>
  <v-app>
    <NavigationDrawer v-model="layout" />
    <AppBar v-model="layout" :title="title" />

    <v-content>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-content>

    <Footer :inset="layout.clipped" />
  </v-app>
</template>

<script>
import Footer from '~/components/default_layout/Footer.vue'
import NavigationDrawer from '~/components/default_layout/NavigationDrawer.vue'
import AppBar from '~/components/default_layout/AppBar.vue'

export default {
  components: {
    Footer, NavigationDrawer, AppBar
  },
  data () {
    return {
      layout: {
        clipped: true,
        drawer: true,
        miniVariant: false
      },
      title: 'Premade Layout'
    }
  }
}
</script>
