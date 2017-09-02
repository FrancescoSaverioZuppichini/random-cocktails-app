<template>
<v-app light>
  <main>
    <v-container fluid>
        <cocktails></cocktails>
    </v-container>
  </main>
  <v-footer :fixed="fixed">
    <span>&copy; 2017 Francesco Saverio Zuppichini</span>
  </v-footer>
</v-app>
</template>

<script>
import Cocktails from './components/Cocktails/Cocktails.vue'

export default {
  components: {
    Cocktails
  },
  data() {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
