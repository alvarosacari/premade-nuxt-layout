<template>
  <v-layout>
    <v-flex xs12>
      <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-card-text>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ab possimus quibusdam sed recusandae tempora a perferendis nostrum. Esse impedit ducimus quas aliquam cumque ut laudantium culpa odio. In, consectetur esse.</p>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>

export default {
  components: { }
}
</script>
