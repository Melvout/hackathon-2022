<template>
  <v-container>
    <v-card id="modal">
      <v-form v-model="valid">
        <h3>Suggestions for the order n°{{ this.alertId }}</h3>

        <br />

        <v-select
          v-model="selectedSolution"
          :items="suggestions"
          :rules="[(v) => !!v || 'You must choose an item.']"
          label="Choose a solution."
          required
        ></v-select>
        <v-card-text>
          If none of the previous solutions fits your need, contact us at : +351
          21 953 95 00
        </v-card-text>

        <v-btn :disabled="!valid" color="info" class="mr-4" @click="validate">
          Validate
        </v-btn>
        <v-btn color="secondary" class="mr-4" @click="cancel"> Cancel </v-btn>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "ProposalsComponent",

  props: ["alertId"],

  data: () => ({
    valid: false,

    selectedSolution: null,
    suggestions: [
      "Deliver on [DATE].",
      "Keep in the warehouse for [X] days.",
      "Cancel the delivery.",
    ],
  }),
  methods: {
    validate() {
      this.$emit("proposals-component:close-dialog");
      this.$emit("proposals-component:validate-modification", [this.alertId]);
    },
    cancel() {
      this.$emit("proposals-component:close-dialog");
    },
  },
};
</script>

<style scoped>
#modal {
  padding: 15px;
  height: auto;
  width: 60vw;
  background-color: #ececec;
}
</style>