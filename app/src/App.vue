<template>
  <v-app>
    <v-main>
      <v-app-bar id="navBar">
        <v-img
          :src="require('./assets/stef_logo.jpg')"
          max-height="64"
          max-width="128"
          contain
        ></v-img>
        <v-btn @click="showPage('modifPage')"
          ><v-icon icon="mdi-pencil"></v-icon> Modification</v-btn
        >
        <v-btn @click="showPage('alertPage')"
          ><v-icon icon="mdi-database"></v-icon> My alerts</v-btn
        >
        <v-btn @click="showPage('settingsPage')"
          ><v-icon icon="mdi-account-cog"></v-icon> Notifications
          settings</v-btn
        >
        <v-icon
          icon="mdi-account-box-outline"
          size="large"
          style="position: absolute; right: 0; color: white"
        ></v-icon>
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
.v-icon {
  margin-right: 5px;
}
.v-img {
  border: 1px solid #005aaa;
}
</style>
