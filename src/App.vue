<template>
  <v-app>
    <v-navigation-drawer app temporary v-model="sideNav">
      <v-list>
         <router-link class="uppercase" to="/" tag="span" style="cursor: pointer">
        <img class="img2" src="./assets/logo2.jpg" alt="">
         </router-link>
        <v-list-tile
          v-for="item in menuItems"
          :key="item.title"
          :to="item.link">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>{{ item.title }}</v-list-tile-content>
        </v-list-tile>
        <v-list-tile
          v-if="userIsAuthenticated"
          @click="onLogout">
          <v-list-tile-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>Logout</v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar dark class="primary">
      <v-toolbar-side-icon
        @click.stop="sideNav = !sideNav"
        class="hidden-sm-and-up "></v-toolbar-side-icon>
      <v-toolbar-title>
        <router-link  class="uppercase" to="/" tag="span" style="cursor: pointer">
        <img class="img" src="./assets/logo2.jpg" alt="">
              Events
        </router-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
        <v-btn
          flat
          v-for="item in menuItems"
          :key="item.title"
          :to="item.link">
          <v-icon left dark>{{ item.icon }}</v-icon>
          {{ item.title }}

        </v-btn>
        <v-btn
          v-if="userIsAuthenticated"
          flat
          @click="onLogout">
          <v-icon left dark>exit_to_app</v-icon>
          Logout

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
          {icon: 'face', title: 'Sign up', link: '/signup'},
          {icon: 'lock_open', title: 'Sign in', link: '/signin'}
        ]
        if (this.userIsAuthenticated) {
          menuItems = [
            {icon: 'supervisor_account', title: 'View Events', link: '/meetups'},
            {icon: 'room', title: 'Organize Event', link: '/meetup/new'},
            {icon: 'person', title: 'Profile', link: '/profile'}
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
        this.$store.dispatch('logout')
      }
    }
  }
</script>

<style lang="stylus">

  @import './stylus/main'

    html { overflow-y:auto }

    .radius {
  border-radius: 100px;
}

.uppercase {
    text-transform: uppercase;
    letter-spacing: 17px;
    font-size: 20px !important;
    font-weight: bolder;
    margin-top: 10px !important;
}

.img {
  height: 50px !important;
  width: 50px !important;
  margin-top: 10px !important;
  margin-bottom: 0px !important;
  margin-left: 10px !important;
  position: relative !important;
}

.img2 {
  margin-top:15px  !important;
  margin-left: 130px !important;
  height: 50px !important;
  width: 50px !important;
  position: relative !important;
}
</style>
