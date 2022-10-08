<template>
  <v-container>
    <br />
    <v-table fixed-header height="300px">
      <thead>
        <tr>
          <th class="text-left">Order</th>
          <th class="text-left">Cause</th>
          <th class="text-left">Status</th>
          <th class="text-left">Date</th>
          <th class="text-left">Required action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="alertOnOrder in alertOnOrdersData" :key="alertOnOrder.id">
          <td>{{ alertOnOrder.id }}</td>
          <td>{{ alertOnOrder.cause }}</td>
          <td>{{ alertOnOrder.state }}</td>
          <td>{{ alertOnOrder.date }}</td>
          <td v-if="alertOnOrder.requiredAction == 0">Action 1</td>
          <td v-else-if="alertOnOrder.requiredAction == 1">
            <v-btn icon size="25" @click="showAlert()">
              <v-icon size="20">mdi-exclamation</v-icon>
            </v-btn>
          </td>
          <td v-else-if="alertOnOrder.requiredAction == 2">Action 3</td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script>
import alertOnOrdersData from "@/resources/alertOnOrders.json";
export default {
  name: "AlertComponent",

  data: () => ({
    alertOnOrdersData: alertOnOrdersData,
  }),
  methods: {
    showAlert: () => {
      alert("OK");
    },
  },
};
</script>
