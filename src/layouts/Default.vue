<template>
  <v-app class="grey lighten-3">
    <v-app-bar
      app
      dark
      elevation="1"
      color="#fcb69f"
      src="https://picsum.photos/id/1064/1920/1080"
    >
      <v-app-bar-nav-icon @click.stop="sideBar = !sideBar"></v-app-bar-nav-icon>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-navigation-drawer
      app
      v-model="sideBar"
      :mini-variant.sync="mini"
      class="grey darken-2"
      elevation="1"
    >
      <v-list dense dark color="grey darken-2">
        <v-list-item>
          <v-list-item-action>
            <v-icon dense @click.stop="sideBar = !sideBar" color="white"
              >mdi-chevron-left</v-icon
            >
          </v-list-item-action>
          <v-icon>mdi-dots-horizontal-circle</v-icon>
          <v-list-item-title><h1 class="h1">Menu</h1></v-list-item-title>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-list-item class="px4" @click.stop="mini = !mini">
        <v-list-item-avatar>
          <v-icon color="white">mdi-account</v-icon>
        </v-list-item-avatar>
        <v-list-item-content>Gustavo Henrique</v-list-item-content>
        <v-btn icon small>
          <v-icon color="white">mdi-chevron-left</v-icon>
        </v-btn>
      </v-list-item>
      <v-divider></v-divider>
      <v-list>
        <v-list-item v-for="item of items" :key="item.title" link :to="item.to">
          <v-list-item-icon>
            <v-icon color="white"> {{ item.icon }} </v-icon>
          </v-list-item-icon>
          <v-list-item-content>{{ item.title }}</v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <router-view></router-view>
    </v-main>

    <v-footer app><span>Meu site &copy;2021</span> </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      sideBar: false,
      mini: false,
      items: [
        {
          title: "Home",
          icon: "mdi-home",
          to: "/",
        },
        {
          title: "Perfil",
          icon: "mdi-account-question",
          to: "/perfil",
        },
        {
          title: "Saida",
          icon: "mdi-exit-to-app",
          to: "/login",
        },
      ],
    };
  },
};
</script>

<style></style>
