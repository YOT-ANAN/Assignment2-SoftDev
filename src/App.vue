<template>
  <v-app style="font-family: 'Kanit', sans-serif;">
    <v-navigation-drawer fixed temporary v-model="sideNav">
      <v-list>
        <v-list-tile
        v-for="item in menuItems"
        :key="item.title"
        router
        :to="item.link"
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>{{ item.title }}</v-list-tile-content>
        </v-list-tile>
        <v-list-tile v-if="userIsAuthenticated"
        @click="onLogout">
          <v-list-tile-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>ออกจากระบบ</v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar dark class="primary">
      <v-toolbar-side-icon @click.native.stop="sideNav = !sideNav" class="hidden-sm-and-up"></v-toolbar-side-icon>
      <v-toolbar-title>
        <router-link to="/" tag="span" style="cursor: pointer"><v-icon>import_contacts</v-icon>
        FunRead</router-link>
      </v-toolbar-title>

      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
        <v-btn flat
        v-for="item in menuItems"
        :key="item.title"
        router
        :to="item.link"
        >
          <v-icon left dark>{{ item.icon }}</v-icon>
          {{ item.title }}</v-btn>
        <v-btn
          v-if="userIsAuthenticated"
          flat
          @click="onLogout">
          <v-icon left dark>exit_to_app</v-icon>
          ออกจากระบบ
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <main>
      <router-view></router-view>
    </main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      sideNav: false
    }
  },
  computed: {
    menuItems () {
      let menuItems = [
        { icon: 'face', title: 'สมัครสมาชิก', link: '/signup' },
        { icon: 'lock_open', title: 'เข้าสู่ระบบ', link: '/signin' },
       
      ]
      if (this.userIsAuthenticated) {
        menuItems = [
          { icon: 'book', title: 'อ่านการ์ตูนทั้งหมด', link: '/funreads' },
          { icon: 'library_add', title: 'เพิ่มการ์ตูน', link: '/funread/new' },
          { icon: 'face', title: 'สมาชิกในกลุ่ม', link: '/member' }
        ]
      }
      return menuItems
    },
    userIsAuthenticated () {
      return this.$store.getters.user !== null && this.$store.getters.user !== undefined
    }
  },
  methods: {
    onLogout () {
      this.$store.dispatch('logout').then(
    () => {
      this.$router.push('/signin')
      this.clearAll()
        }
      )
    }
  }
}
</script>
