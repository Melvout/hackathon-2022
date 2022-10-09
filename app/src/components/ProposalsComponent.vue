<template>
  <v-container id="modal"> Jean-Marie Bigard Ma Couillasse </v-container>
</template>

<script>
export default {
  name: "ProposalsComponent",

  data: () => ({}),
  methods: {
    validate: () => {
      alert("OK");
    },
  },
};
</script>

<style scoped>
#modal {
  height: 60vh;
  width: 60vw;
  background-color: #ececec;
}
</style>