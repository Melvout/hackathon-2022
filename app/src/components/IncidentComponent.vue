<template>
  <v-container>
    <h3>Déclarer un incident</h3>

    <v-form ref="form" v-model="valid" lazy-validation>

      <v-select
        v-model="selectedOrder"
        :items="orders"
        :rules="[(v) => !!v || 'Numéro de commande requis.']"
        label="Numéro de commande"
        required
      ></v-select>

      <v-select
        v-model="selectedType"
        :items="issueTypes"
        :rules="[(v) => !!v || 'Type de modification requis.']"
        label="Type de modification"
        required
      ></v-select>

      <v-text-field
      v-model="date"
      type="datetime-local"
      label="Date"
      required
    ></v-text-field>

    <v-text-field
      v-model="address"
      type="address"
      label="Adresse"
      required
    ></v-text-field>

    <v-textarea
    v-model="comment"
    label="Commentaire"
    ></v-textarea>

      
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        Validate
      </v-btn>

    </v-form>
  
  </v-container>
</template>
  
<script>

export default {
  name: "IncidentComponent",

  data: () => ({
    valid: true,

    selectedOrder: null,
    orders: ["124897520167", "124897520103", "12489752018", "124897520146"],

    selectedType: null,
    issueTypes: ["Changement de coordonnées (date, heure, adresse...)", "Autres (précisez en commentaire)"],

    date: null,
    address: null,
    comment: null,
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
    },
  },
};
</script>
  
<style scoped>
</style>