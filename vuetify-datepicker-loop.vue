<template>
  <div id="app">
    <v-app>
      <v-content>
        <v-container>
          <v-flex v-for="(n, i) in 3" :key="i">
            <v-row>
              <v-col cols="12" sm="6" md="6">
                <v-menu
                  ref="DOBMenu[i]"
                  v-model="DOBMenu[i]"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      v-model="DOB[i]"
                      v-on="on"
                      :rules="nameRules"
                      clearable
                      hide-details
                      dense
                      readonly
                      label="Birthday date"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    ref="picker"
                    v-model="DOB[i]"
                    :min="getMinDOB"
                    :max="getMaxDOB"
                    @change="DOBMenu[i] = false"
                  ></v-date-picker>
                </v-menu>
              </v-col>
            </v-row>
          </v-flex>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import moment from "moment";

export default {};

new Vue({
  el: "#app",
  vuetify: new Vuetify(),
  data: () => ({
    nameRules: [v => !!v || "Required"],
    DOBMenu: [],
    DOB: []
  }),
  computed: {
    getMinDOB() {
      // var minDOB = moment(moment(), "YYYY-MM-DD").add(-36501, "days");
      // var day = minDOB.format("DD");
      // var month = minDOB.format("MM");
      // var year = minDOB.format("YYYY");
      // return year + "-" + month + "-" + day;
    },
    getMaxDOB() {
      // var maxDOB = new Date();
      // return maxDOB.toISOString().substr(0, 10);
    }
  },

  watch: {
    DOBMenu(val, picker) {
      val &&
        setTimeout(
          () =>
            (this.$refs.picker[this.$refs.picker.length - 1].activePicker =
              "YEAR")
        );
    }
  }
});
</script>