<template>
  <v-container>
    <v-table fixed-header height="300px">
      <thead>
        <tr>
          <th class="text-left">Order</th>
          <th class="text-left">Cause</th>
          <th class="text-left">State</th>
          <th class="text-left">Date</th>
          <th class="text-left">Required action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="order in orders" :key="order.id">
          <td>{{ order.id }}</td>
          <td>{{ order.cause }}</td>
          <td>{{ order.state }}</td>
          <td>{{ order.date }}</td>
          <td v-if="order.requiredAction == 0">Action 1</td>
          <td v-else-if="order.requiredAction == 1">
            <v-btn icon size="25" @click="showAlert()">
              <v-icon size="20">mdi-exclamation</v-icon>
            </v-btn>
          </td>
          <td v-else-if="order.requiredAction == 2">Action 3</td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>
  
  <script>
import ordersData from "@/resources/orders.json";
export default {
  name: "AlertComponent",

  data: () => ({
    orders: ordersData,
  }),
  methods: {
    showAlert: () => {
      alert("OK");
    },
  },
};
</script>
