<template>
  <v-app>
    <v-main>
      <v-app-bar id="navBar">
        <v-btn @click="alertPage = false">Modification</v-btn>
        <v-btn @click="alertPage = true">Mes alertes</v-btn>
      </v-app-bar>
      <AlertComponent v-if="alertPage" />
      <IncidentComponent v-else />
    </v-main>
  </v-app>
</template>

<script>
import AlertComponent from "./components/AlertComponent.vue";
import IncidentComponent from "./components/IncidentComponent.vue";

export default {
  name: "App",

  components: {
    AlertComponent,
    IncidentComponent,
  },

  data: () => ({
    alertPage: false,
  }),

  methods: {},
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
