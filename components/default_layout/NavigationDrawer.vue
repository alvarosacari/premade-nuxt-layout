<template>
  <v-navigation-drawer
    v-model="value.drawer"
    :mini-variant="value.miniVariant"
    :clipped="value.clipped"
    fixed
    app
  >
    <v-img :aspect-ratio="16/9" :src="require('~/assets/images/material.jpg')">
      <v-row align="end" class="lightbox fill-height">
        <v-col class="pb-0">
          <v-list dark class="pa-0">
            <v-list-item two-line>
              <v-list-item-avatar>
                <v-img :src="require('~/assets/images/face.jpg')" />
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title v-text="user.name" />
                <v-list-item-subtitle v-text="user.email" />
              </v-list-item-content>

              <v-list-item-action>
                <v-menu offset-y open-on-hover>
                  <template v-slot:activator="{ on }">
                    <v-btn icon v-on="on">
                      <v-icon>
                        mdi-dots-vertical
                      </v-icon>
                    </v-btn>
                  </template>
                  <v-list nav dense>
                    <v-list-item
                      v-for="(item, index) in userMenu"
                      :key="index"
                      @click="() => {}"
                    >
                      <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                      </v-list-item-content>
                      <v-list-item-icon>
                        <v-icon>{{ item.icon }}</v-icon>
                      </v-list-item-icon>
                    </v-list-item>
                  </v-list>
                </v-menu>
              </v-list-item-action>
            </v-list-item>
          </v-list>
        </v-col>
      </v-row>
    </v-img>

    <v-list dense nav>
      <template v-for="(item,i) in items">
        <template v-if="!item.items">
          <v-list-item
            :key="`list${i}`"
            :to="item.to"
            exact
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </template>
        <template v-else>
          <v-list-group
            :key="`group${i}`"
            :prepend-icon="item.icon"
            :value="item.expand"
            no-action
          >
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </template>
            <template v-for="(subItem,j) in item.items">
              <template v-if="!subItem.items">
                <v-list-item
                  :key="`subItem${j}`"
                  :to="subItem.to"
                  exact
                >
                  <v-list-item-content>
                    <v-list-item-title>{{ subItem.title }}</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </template>
              <template v-else>
                <v-list-group
                  :key="`subGroup${j}`"
                  no-action
                  sub-group
                  :value="subItem.expand"
                >
                  <template v-slot:activator>
                    <v-list-item-content>
                      <v-list-item-title>{{ subItem.title }}</v-list-item-title>
                    </v-list-item-content>
                  </template>
                  <template v-for="(subSubItem, k) in subItem.items">
                    <v-list-item
                      :key="`subSubItem${k}`"
                      :to="subSubItem.to"
                      exact
                    >
                      <v-list-item-title>{{ subSubItem.title }}</v-list-item-title>
                      <v-list-item-icon>
                        <v-icon>{{ subSubItem.icon }}</v-icon>
                      </v-list-item-icon>
                    </v-list-item>
                  </template>
                </v-list-group>
              </template>
            </template>
          </v-list-group>
        </template>
      </template>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      default () { return {} }
    }
  },

  data () {
    return {
      user: {
        name: 'Alvaro S.',
        email: 'alvaro.sacari@gmail.com'
      },

      userMenu: [
        { title: 'Profile', icon: 'mdi-account' },
        { title: 'Logout', icon: 'mdi-exit-to-app' }
      ]
    }
  },

  computed: {
    items () {
      let items = [
        {
          title: 'Home',
          icon: 'mdi-home',
          to: '/'
        },
        {
          title: 'Banners',
          icon: 'mdi-panorama',
          expand: false,
          items: [
            {
              title: 'See all',
              to: '/banners'
            },
            {
              title: 'Create new',
              to: '/banners/create'
            }
          ]
        },
        {
          title: 'Articles',
          icon: 'mdi-library-books',
          expand: false,
          items: [
            {
              title: 'See all',
              to: '/articles'
            },
            {
              title: 'Create new',
              to: '/articles/create'
            },
            {
              title: 'Tags',
              expand: false,
              items: [
                {
                  title: 'See all',
                  to: '/tags'
                },
                {
                  title: 'Create new',
                  to: '/tags/create'
                }
              ]
            }
          ]
        }
      ]

      items = this.setExpandValue(items)

      return items
    }
  },

  methods: {
    setExpandValue (items) {
      const routePath = this.$route.path

      return items.map((item) => {
        if (!item.hasOwnProperty('items')) {
          return item
        }

        item.items.map((subitem) => {
          if (subitem.to && subitem.to === routePath) {
            item.expand = true
          }

          if (!subitem.hasOwnProperty('items')) {
            return subitem
          }

          subitem.items.map((subsubitem) => {
            if (subsubitem.to && subsubitem.to === routePath) {
              item.expand = true
              subitem.expand = true
            }

            return subsubitem
          })

          return subitem
        })

        return item
      })
    }
  }
}
</script>

<style lang="scss">
.v-navigation-drawer {
  transition: none !important;
}

.lightbox {
  box-shadow: 0 0 20px inset rgba(0, 0, 0, 0.2);
  background-image: linear-gradient(to top, rgba(0, 0, 0, 0.4) 0%, transparent 72px);
}
</style>
