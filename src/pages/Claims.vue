<template>
  <v-container fluid grid-list-xl>
    <v-layout>
      <v-flex md11 class="bread-size">Claims Request</v-flex>
      <v-flex md1><v-icon color="green" @click="$router.push({ name: 'Search' })">search</v-icon></v-flex>
      <v-flex md1><v-icon color="green" @click="$router.push({ name: 'Home' })">home</v-icon></v-flex>
    </v-layout>
    <v-tabs>
      <v-tab class="table-header-style font-weight-bold font-roboto">Pending Request</v-tab>
      <v-tab class="table-header-style font-weight-bold font-roboto">Approved</v-tab>
      <v-tab class="table-header-style font-weight-bold font-roboto">In Progress</v-tab>
      <v-tab class="table-header-style font-weight-bold font-roboto">Rejected</v-tab>
      <v-tab class="table-header-style tab-style"></v-tab>
      <v-tab class="table-header-style tab-style"></v-tab>
      <v-tab class="table-header-style tab-style"></v-tab>
      <v-spacer class="table-header-style"></v-spacer>
      <v-tab-item>
        <v-card flat class="table-header-style card-style">
          <v-layout class="font-weight-bold font-roboto">
            <v-flex md5>Patient Details</v-flex>
            <v-flex md2>Network</v-flex>
            <v-flex md3>Current Phase</v-flex>
            <v-flex md3>Total Amount</v-flex>
            <v-flex md3>Patient Amount</v-flex>
            <v-flex md3>Billed To Insurance</v-flex>
          </v-layout>
        </v-card>
        <v-card class="card-style rounded" v-for="statement in statements" v-bind:key="statement">
          <v-card-text v-if="(statement.CurrentPhase == 'Ready to Process') || (statement.CurrentPhase == 'Ready to Service')">
            <v-layout>
              <v-flex
                md5
                class="font-weight-bold font-roboto patient-size"
              >{{statement.PatientName}}</v-flex>
              <v-flex md2></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3 class="date-size">{{statement.Date}}</v-flex>
            </v-layout>
            <v-layout class="font-poppins">
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">ID:</span>
                {{statement.Id}}
                <br />
                <span class="custom-font-color font-weight-bold">Provider:</span>
                {{statement.Provider}}
                <br />
                <span class="custom-font-color font-weight-bold">Description:</span>
                {{statement.Description}}
              </v-flex>
              <v-flex md2 class="network font-weight-bold">{{statement.NetworkInOut}}</v-flex>
              <v-flex md3>{{statement.CurrentPhase}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.TotalCharge}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.PatientAmount}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.BilledToInsurance}}</v-flex>
            </v-layout>
            <br />
            <hr class="hr-class" />
            <br />
            <v-layout>
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">Attachment:</span> InboundAdvance.PDF
                <v-icon color="green">save_alt</v-icon>
              </v-flex>
              <v-flex md2></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3>
                <v-btn
                  class="success btn-size"
                  v-on:click="sendToThirdParty(statement.Id)"
                  @click.stop="dialog = true"
                >Send Claim</v-btn>
              </v-flex>
              <v-dialog v-model="dialog" max-width="350">
                <v-card text-center>
                  <v-card-title class="headline">Claim Sent</v-card-title>
                  <v-card-text>Claim is sent to the TPA and logged to the blockchain ledger</v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn class="success" text @click="dialog = false">Done</v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-tab-item>

      <v-tab-item>
        <v-card flat class="table-header-style card-style">
          <v-layout class="font-weight-bold font-roboto">
            <v-flex md5>Patient Details</v-flex>
            <v-flex md2>Network</v-flex>
            <v-flex md3>Current Phase</v-flex>
            <v-flex md3>Total Amount</v-flex>
            <v-flex md3>Patient Amount</v-flex>
            <v-flex md3>Billed To Insurance</v-flex>
          </v-layout>
        </v-card>
        <v-card class="card-style rounded" v-for="statement in statements" v-bind:key="statement">
          <v-card-text v-if="statement.CurrentPhase == 'Approved'">
            <v-layout>
              <v-flex
                md5
                class="font-weight-bold font-roboto patient-size"
              >{{statement.PatientName}}</v-flex>
              <v-flex md2></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3 class="date-size">{{statement.Date}}</v-flex>
            </v-layout>
            <v-layout class="font-poppins">
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">ID:</span>
                {{statement.Id}}
                <br />
                <span class="custom-font-color font-weight-bold">Provider:</span>
                {{statement.Provider}}
                <br />
                <span class="custom-font-color font-weight-bold">Description:</span>
                {{statement.Description}}
              </v-flex>
              <v-flex md2 class="network font-weight-bold">{{statement.NetworkInOut}}</v-flex>
              <v-flex md3>{{statement.CurrentPhase}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.TotalCharge}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.PatientAmount}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.BilledToInsurance}}</v-flex>
            </v-layout>
            <br />
            <hr class="hr-class" />
            <br />
            <v-layout>
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">Attachment:</span> InboundAdvance.PDF
                <v-icon color="green">save_alt</v-icon>
              </v-flex>
              <v-flex md4></v-flex>
              <v-flex md4></v-flex>
              <v-flex md4></v-flex>
              <v-flex md2>
                <v-icon color="green">check_circle_outline</v-icon>
                <span style="color:green">Approved</span>
              </v-flex>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-tab-item>

      <v-tab-item>
        <v-card flat class="table-header-style card-style">
          <v-layout class="font-weight-bold font-roboto">
            <v-flex md5>Patient Details</v-flex>
            <v-flex md2>Network</v-flex>
            <v-flex md3>Current Phase</v-flex>
            <v-flex md3>Total Amount</v-flex>
            <v-flex md3>Patient Amount</v-flex>
            <v-flex md3>Billed To Insurance</v-flex>
          </v-layout>
        </v-card>
        <v-card class="card-style rounded" v-for="statement in statements" v-bind:key="statement">
          <v-card-text v-if="statement.CurrentPhase == 'Processing'">
            <v-layout>
              <v-flex
                md5
                class="font-weight-bold font-roboto patient-size"
              >{{statement.PatientName}}</v-flex>
              <v-flex md2></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3 class="date-size">{{statement.Date}}</v-flex>
            </v-layout>
            <v-layout class="font-poppins">
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">ID:</span>
                {{statement.Id}}
                <br />
                <span class="custom-font-color font-weight-bold">Provider:</span>
                {{statement.Provider}}
                <br />
                <span class="custom-font-color font-weight-bold">Description:</span>
                {{statement.Description}}
              </v-flex>
              <v-flex md2 class="network font-weight-bold">{{statement.NetworkInOut}}</v-flex>
              <v-flex md3>{{statement.CurrentPhase}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.TotalCharge}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.PatientAmount}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.BilledToInsurance}}</v-flex>
            </v-layout>
            <br />
            <hr class="hr-class" />
            <br />
            <v-layout>
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">Attachment:</span> InboundAdvance.PDF
                <v-icon color="green">save_alt</v-icon>
              </v-flex>
              <v-flex md4></v-flex>
              <v-flex md4></v-flex>
              <v-flex md4></v-flex>
              <v-flex md2>
                <v-icon color="orange">history</v-icon>
                <span style="color:orange">Processing</span>
              </v-flex>
            </v-layout>
            <br />
            <v-stepper alt-labels>
              <v-stepper-header>
                <v-stepper-step step complete color="green">
                  Provider
                  <small>Claim Generated</small>
                </v-stepper-step>
                <v-divider></v-divider>
                <v-stepper-step step :complete="(statement.CurrentPhase == 'Processing') || (statement.CurrentPhase == 'Approved')" color="green">
                  Aspira
                  <small>Claim Sent To TPA</small>
                </v-stepper-step>
                <v-divider></v-divider>
                <v-stepper-step step :complete="(statement.CurrentPhase == 'Approved')" color="green">
                  TPA
                  <small>Cost Negotiation</small>
                </v-stepper-step>
                <v-divider></v-divider>
                <v-stepper-step step :complete="(statement.CurrentPhase == 'Approved')" color="green">
                  Aspira
                  <small>Paid</small>
                </v-stepper-step>
                <v-divider></v-divider>
                <v-stepper-step step :complete="(statement.CurrentPhase == 'Approved')" color="green">
                  Patient
                  <small>Claim Ready</small>
                </v-stepper-step>
              </v-stepper-header>
            </v-stepper>
          </v-card-text>
        </v-card>
      </v-tab-item>

      <v-tab-item>
        <v-card flat class="table-header-style card-style">
          <v-layout class="font-weight-bold font-roboto">
            <v-flex md5>Patient Details</v-flex>
            <v-flex md2>Network</v-flex>
            <v-flex md3>Current Phase</v-flex>
            <v-flex md3>Total Amount</v-flex>
            <v-flex md3>Patient Amount</v-flex>
            <v-flex md3>Billed To Insurance</v-flex>
          </v-layout>
        </v-card>
        <v-card class="card-style rounded" v-for="statement in statements" v-bind:key="statement">
          <v-card-text v-if="statement.CurrentPhase == 'Rejected'">
            <v-layout>
              <v-flex
                md5
                class="font-weight-bold font-roboto patient-size"
              >{{statement.PatientName}}</v-flex>
              <v-flex md2></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3></v-flex>
              <v-flex md3 class="date-size">{{statement.Date}}</v-flex>
            </v-layout>
            <v-layout class="font-poppins">
              <v-flex md5>
                <span class="custom-font-color font-weight-bold">ID:</span>
                {{statement.Id}}
                <br />
                <span class="custom-font-color font-weight-bold">Provider:</span>
                {{statement.Provider}}
                <br />
                <span class="custom-font-color font-weight-bold">Description:</span>
                {{statement.Description}}
              </v-flex>
              <v-flex md2 class="network font-weight-bold">{{statement.NetworkInOut}}</v-flex>
              <v-flex md3>{{statement.CurrentPhase}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.TotalCharge}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.PatientAmount}}</v-flex>
              <v-flex
                md3
                v-for="diag in statement.diagnosisArr"
                v-bind:key="diag"
              >${{diag.BilledToInsurance}}</v-flex>
            </v-layout>
            <br />
            <hr class="hr-class" />
            <br />
            <v-layout>
              <v-flex md7>
                <span class="custom-font-color font-weight-bold">Reason:</span> Reason: Lorem ipsum dolor sit amet, consectetu.
              </v-flex>
              <v-flex md4></v-flex>
              <v-flex md4></v-flex>
              <v-flex md2>
                <v-icon color="red">highlight_off</v-icon>
                <span style="color:red">Rejected</span>
              </v-flex>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs>
    <!-- <v-layout>
      <v-flex class="spacer-width"></v-flex>
    </v-layout> -->
  </v-container>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      tab: null,
      statements: [],
      statementID: null,
      tabs: 3,
      dialog: false,
      step2: true
    };
  },
  mounted() {
    axios.get("http://132.145.202.167:3003/statements").then(response => {
      this.statements = response.data;
    });
  },
  methods: {
    sendToThirdParty(statementID) {
      axios
        .patch("http://132.145.202.167:3003/statements/" + statementID, {
          currentPhase: "Processing"
        })
        .then(response => {
          console.log(
            "Sent " + statementID + " for third party processing successfully."
          );
          window.location.reload();
        });
    }
  }
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css?family=Poppins");
@import url("https://fonts.googleapis.com/css?family=Roboto");
.card-style {
  margin-top: 3%;
  margin-left: 3%;
  margin-right: 3%;
}
.font-roboto {
  font-family: "Roboto", sans-serif;
}
.table-header-style {
  background-color: rgba(239, 244, 242);
}
.tab-style {
  width: 20%;
}
.rounded {
  border-radius: 2%;
}
.patient-size {
  font-size: 17px;
}
.date-size {
  font-size: 11px;
  font-family: "Poppins", sans-serif;
}
.hr-class {
  opacity: 0.2;
}
.font-poppins {
  font-family: "Poppins", sans-serif;
  font-size: 13px;
}
.custom-font-color {
  color: #4e8416;
}
.network {
  color: #d99700;
}
.btn-size {
  width: 90%;
}
.spacer-width {
  margin-bottom: 75%;
}
.bread-size {
  font-size: 22px;
  font-weight: bold;
}
</style>
