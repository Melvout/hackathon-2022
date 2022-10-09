<template>
  <v-container>
    <v-table fixed-header height="300px" style="overflow: hidden">
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
        <transition-group
          name="custom-classes-transition"
          enter-active-class="animated tada"
          leave-active-class="animated bounceOutRight"
        >
          <tr
            v-for="(alertOnOrder, index) in alertOnOrdersData"
            :key="alertOnOrder.id"
          >
            <td>{{ alertOnOrder.id }}</td>
            <td>{{ alertOnOrder.cause }}</td>
            <td>{{ alertOnOrder.state }}</td>
            <td>{{ alertOnOrder.date }}</td>
            <td v-if="alertOnOrder.requiredAction == 0">
              <v-btn icon size="25" @click="validateModification(index)">
                <v-icon size="20">mdi-check</v-icon>
              </v-btn>
            </td>
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
            <td v-else-if="alertOnOrder.requiredAction == 2">
              <v-btn icon size="25" @click="validateModification(index)">
                <v-icon size="20">mdi-check</v-icon>
              </v-btn>
            </td>
          </tr>
        </transition-group>
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
      this.alertOnOrdersData.splice(alertId, 1);
    },
  },
  components: { ProposalsComponent },
};
</script>
<style>
.v-table__wrapper {
  overflow: hidden !important;
}
</style>

<style scoped>
@import url("https://cdn.jsdelivr.net/npm/animate.css@3.5.1");
</style>>
