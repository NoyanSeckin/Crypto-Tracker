<template>
  <v-app>
    <Navbar app />
    <!-- <AutoComplete /> -->
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "./components/Navbar";
// import AutoComplete from "./components/AutoComplete.vue";

export default {
  name: "App",
  components: {
    Navbar,
    // AutoComplete,
  },

  data: () => ({
    //
  }),
};
</script>
