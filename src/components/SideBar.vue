<template>
  <v-navigation-drawer permanent class="sidebar">
      <v-divider></v-divider>

       <v-list>

      <v-list-group
        :value="true"
        prepend-icon="mdi-account-circle"
      >
        <template v-slot:activator>
          <v-list-item-title>Catalogue</v-list-item-title>
        </template>

          <v-list-item
            v-for="([title, icon], i) in cruds"
            :key="i"
            link
          >
            <v-list-item-title v-text="title"></v-list-item-title>

            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>
    </v-list>
    </v-navigation-drawer>
</template>

<script>
import { mapActions, mapState } from 'vuex'
export default {
  props: {
    source: String
  },
  data () {
    return {
      cruds: [
        ['My Products', 'mdi-file-outline']
      ],
      sidebarWidth: 240,
      sidebarMinWidth: 96
    }
  },
  computed: {
    ...mapState(['drawer']),
    DRAWER_STATE: {
      get () {
        return this.drawer
      },
      set (newValue) {
        if (newValue === this.drawer) return
        this.TOGGLE_DRAWER()
      }
    }
  },
  methods: {
    ...mapActions(['TOGGLE_DRAWER'])
  }
}
</script>
<style scoped>
.sidebar {
    height: 100vh !important;
    z-index: 1;
}
</style>
