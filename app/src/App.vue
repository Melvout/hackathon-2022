<template>
  <v-app>
    <v-main>
      <v-app-bar id="navBar">
        <v-btn @click="showPage('modifPage')">Modification</v-btn>
        <v-btn @click="showPage('alertPage')">My alerts</v-btn>
        <v-btn @click="showPage('settingsPage')">Notifications settings</v-btn>
      </v-app-bar>
      <AlertComponent v-if="alertPage" />
      <IncidentComponent v-else-if="modifPage" />
      <NotificationSettings v-else />
    </v-main>
  </v-app>
</template>

<script>
import AlertComponent from "./components/AlertComponent.vue";
import IncidentComponent from "./components/IncidentComponent.vue";
import NotificationSettings from "./components/NotificationSettings.vue";

export default {
  name: "App",

  components: {
    AlertComponent,
    IncidentComponent,
    NotificationSettings,
  },

  data: () => ({
    alertPage: false,
    modifPage: true,
  }),

  methods: {
    showPage(name) {
      switch (name) {
        case "alertPage":
          this.alertPage = true;
          this.modifPage = false;
          break;
        case "modifPage":
          this.modifPage = true;
          this.alertPage = false;
          break;
        default:
          this.alertPage = false;
          this.modifPage = false;
      }
    },
  },
};
</script>
<style scoped>
#navBar {
  background-color: #005aaa;
}
.v-btn {
  color: white;
}
</style>
