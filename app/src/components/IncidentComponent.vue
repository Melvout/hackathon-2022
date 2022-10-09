<template>
  <v-container>
    <v-alert
      id="alert"
      v-if="displaySaveAlert"
      icon="mdi-content-save"
      title="Demande enregistrée"
      type="success"
      density="compact"
    ></v-alert>
    <v-dialog
      id="modal"
      v-model="dialog"
      v-on:click:outside="clickOutside"
      width="unset"
    >
      <template v-slot:activator="{ props }">
        <v-btn color="info" v-bind="props"
          ><v-icon icon="mdi-plus-box" />New modification request</v-btn
        >
      </template>
      <v-card id="formCard">
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-select
            v-model="selectedOrder"
            :items="orders"
            :rules="[(v) => !!v || 'Order number needed']"
            label="Order number"
            required
          ></v-select>

          <v-select
            v-model="selectedType"
            :items="issueTypes"
            :rules="[(v) => !!v || 'Modification type required']"
            label="Modification type"
            required
          ></v-select>

          <v-text-field
            v-model="date"
            type="datetime-local"
            label="New delivery date (fill if needed)"
            required
          ></v-text-field>

          <v-text-field
            v-model="address"
            type="address"
            label="New delivery location (fill if needed)"
            required
          ></v-text-field>

          <v-textarea v-model="comment" label="Comment"></v-textarea>

          <v-btn :disabled="!valid" color="info" class="mr-4" @click="validate">
            Validate
          </v-btn>
          <v-btn color="secondary" class="mr-4" @click="clickOutside">
            Cancel
          </v-btn>
        </v-form>
      </v-card>
    </v-dialog>

    <br />

    <v-table>
      <thead>
        <tr>
          <th class="text-left">Order number</th>
          <th class="text-left">Modification type</th>
          <th class="text-left">New address</th>
          <th class="text-left">New date</th>
          <th class="text-left">Status</th>
          <th class="text-left">Comment</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in demands" :key="item.name">
          <td>{{ item.order }}</td>
          <td>{{ item.type }}</td>
          <td>{{ item.address }}</td>
          <td>{{ item.date }}</td>
          <td v-bind:style="{ color: getStatusColor(item) }">
            {{ item.status }}
          </td>
          <td>{{ item.comments }}</td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script>
export default {
  name: "IncidentComponent",

  data: () => ({
    valid: true,
    dialog: false,

    selectedOrder: null,
    orders: ["124897520167", "124897520103", "12489752018", "124897520146"],

    selectedType: null,
    issueTypes: [
      "Change delivery information (date, hour, address...)",
      "Change products and/or amounts",
      "Other (Use comments field to develop)",
    ],

    date: null,
    address: null,
    comment: null,
    displaySaveAlert: false,
    demands: [
      {
        order: 124897520103,
        type: "Change delivery information",
        address: "Quinta do Anabique, 2625-090 Póvoa de Santa Iria",
        date: "10/10/2022 14:00",
        comments:
          "Stock currently full, asking to delay the delivery by 2 days",
        status: "Pending",
      },
      {
        order: 124897520167,
        type: "Other",
        date: "24/10/2022 10:00",
        address: "Quinta do Anabique, 2625-090 Póvoa de Santa Iria",
        comments: "Can't be here on original date, I have aqua-poney",
        status: "Approved",
      },
      {
        order: 12489752018,
        type: "Change products and/or amounts",
        address: "Quinta do Anabique, 2625-090 Póvoa de Santa Iria",
        date: "12/10/2022 12:00",
        status: "Rejected",
      },
    ],
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
      this.demands.push({
        order: this.selectedOrder,
        date: this.date,
        type: this.selectedType,
        address: this.address,
        comments: this.comment,
        status: "Pending",
      });
      this.displaySaveAlert = true;
      setTimeout(() => (this.displaySaveAlert = false), 2000);
      this.dialog = false;
      this.$refs.form.reset();
    },
    clickOutside() {
      this.$refs.form.reset();
      this.dialog = false;
    },
    getStatusColor(item) {
      switch (item.status) {
        case "Pending":
          return "orange";
        case "Approved":
          return "green";
        case "Rejected":
          return "red";
        default:
          return "black";
      }
    },
  },
};
</script>

<style scoped>
#formCard {
  padding: 20px;
  width: 60vw;
  min-width: 600px;
  margin: auto;
}
#alert {
  margin: 5px 0;
}
.v-icon {
  margin-right: 5px;
}
</style>
