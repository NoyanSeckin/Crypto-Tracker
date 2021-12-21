<template>
  <nav>
    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"> </v-app-bar-nav-icon>
      <v-app-bar-title>
        <span class="grey--text font-weight-medium">Crypto</span>
        <span class="font-weight-bold">Tracker</span>
      </v-app-bar-title>
      <v-spacer></v-spacer>
      <v-btn class="secondary">Sign up</v-btn>
      <v-btn color="grey">Login</v-btn>
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer" class="danger">
      <v-list-item v-for="content in drawerContent" :key="content.title">
        <v-list-item-action>
          <v-icon>
            {{ content.icon }}
          </v-icon>
        </v-list-item-action>
        <v-list-item-title>
          {{ content.title }}
        </v-list-item-title>
      </v-list-item>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      drawer: false,
      drawerContent: [
        { title: "Home", icon: "mdi-home" },
        { title: "About Us", icon: "mdi-information-outline" },
        { title: "Contact", icon: "mdi-email" },
      ],
    };
  },
};
</script>
