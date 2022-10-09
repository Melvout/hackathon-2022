<template>
  <v-container>
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
        <tr
          v-for="(alertOnOrder, index) in alertOnOrdersData"
          :key="alertOnOrder.id"
        >
          <td>{{ alertOnOrder.id }}</td>
          <td>{{ alertOnOrder.cause }}</td>
          <td>{{ alertOnOrder.state }}</td>
          <td>{{ alertOnOrder.date }}</td>
          <td v-if="alertOnOrder.requiredAction == 0">Action 1</td>
          <td v-else-if="alertOnOrder.requiredAction == 1">
            <v-dialog id="modal" v-model="dialog" width="unset">
              <template v-slot:activator="{ props }">
                <v-btn icon size="25" v-bind="props">
                  <v-icon size="20">mdi-exclamation</v-icon>
                </v-btn>
              </template>

              <ProposalsComponent
                @proposals-component:close-dialog="clickOutside()"
                @proposals-component:validate-modification="
                  validateModification($event[0])
                "
                :alertId="index"
              ></ProposalsComponent>
            </v-dialog>
          </td>
          <td v-else-if="alertOnOrder.requiredAction == 2">Action 3</td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script>
import ProposalsComponent from "@/components/ProposalsComponent.vue";
import alertOnOrdersData from "@/resources/alertOnOrders.json";
export default {
  name: "AlertComponent",
  data: () => ({
    index: null,
    alertOnOrdersData: alertOnOrdersData,
    dialog: false,
  }),
  methods: {
    clickOutside() {
      this.dialog = false;
    },
    validateModification(alertId) {
      this.alertOnOrdersData[alertId].state = "Done";
    },
  },
  components: { ProposalsComponent },
};
</script>
