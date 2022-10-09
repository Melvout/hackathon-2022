<template>
  <v-container>
    <br />
    <v-card id="formCard">
      <h3>To receive my notifications</h3>
      <br />
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-select
          v-model="selectedType"
          :items="types"
          label="Communication channel(s)"
          multiple
        ></v-select>

        <v-text-field v-model="email" type="email" label="Email"></v-text-field>

        <v-text-field
          v-model="phoneNumber"
          type="phoneNumber"
          label="Phone number"
        ></v-text-field>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "NotificationsSettings",

  data: () => ({
    selectedType: ["Email"],
    types: ["Email", "Phone number"],
    email: "felonius.gru@stef.com",
    phoneNumber: "",
  }),
  methods: {},
};
</script>

<style>
#formCard {
  padding: 10px;
  width: 1000px;
  margin: auto;
}
</style>
