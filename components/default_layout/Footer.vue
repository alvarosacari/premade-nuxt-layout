<template>
  <v-footer
    color="primary"
    :inset="!inset"
    dark
    app
  >
    <span>
      Premade Layout © {{ year }} Developed by
      <a
        class="white--text"
        :href="github.url"
        target="_blank"
      >{{ github.user }}</a>
    </span>
  </v-footer>
</template>

<script>
export default {
  props: {
    inset: {
      type: Boolean,
      default: false
    }
  },

  data () {
    return {
      github: {
        url: 'https://github.com/alvarosacari',
        user: 'Alvaro Sacari'
      }
    }
  },

  computed: {
    year () {
      return new Date().getFullYear()
    }
  }
}
</script>
