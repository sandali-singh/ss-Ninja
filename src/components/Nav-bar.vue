<template>
  <nav>
    <v-snackbar v-model="snackbar" :timeout="4000" top color="success">
      <span>Awesome! You added a new project</span>
      <v-btn text color="white" @click="snackbar = false">Close</v-btn>
    </v-snackbar>
    <v-app-bar app>
      <v-app-bar-nav-icon
        @click.stop="drawer = !drawer"
        class="grey--text"
      ></v-app-bar-nav-icon>

      <v-toolbar-title class="text-uppercase grey--text">
        <span class="font-weight-light">Sandali</span>
        <span>Singh</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <!--dropdown menu-->

      <v-menu offset-y transition="slide-x-transition">
        <template v-slot:activator="{ on, attrs }">
          <v-btn outlined color="grey" v-bind="attrs" v-on="on">
            <v-icon left>mdi-chevron-down</v-icon>
            <span>Menu</span>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="link in links"
            :key="link.text"
            router
            :to="link.route"
          >
            <v-list-item-title>{{ link.text }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

      <v-btn plain>
        <span class="grey--text"></span>
        Sign Out
        <v-icon right>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" class="primary">
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="100" class="grey lighten-4">
            <img src="/avatar5.png" />
          </v-avatar>
          <p class="white--text mt-4">Sandali Singh</p>
        </v-flex>
        <v-flex class="mt-4 mb-3">
          <pop_up @projectAdded="snackbar = true" />
        </v-flex>
      </v-layout>
      <v-list>
        <v-list-item
          v-for="link in links"
          :key="link.text"
          router
          :to="link.route"
        >
          <v-list-item-icon>
            <v-icon class="white--text">{{ link.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title class="white--text">
              {{ link.text }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
import pop_up from "./pop-up.vue";

export default {
  components: { pop_up },
  data() {
    return {
      drawer: false,
      links: [
        { icon: "mdi-view-dashboard", text: "Dashboard", route: "/" },
        { icon: "mdi-folder", text: "My Projects", route: "/projects" },
        { icon: "mdi-account", text: "Team", route: "/team" },
      ],
      snackbar: false,
    };
  },
};
</script>
