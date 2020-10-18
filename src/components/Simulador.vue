<template>
  <div>
    <v-container class="grey lighten-5 pa-0" fluid>
      <v-layout no-gutters fill-height>
        <v-col>
          <v-stepper v-model="e1">
            <v-stepper-header>
              <v-stepper-step :complete="e1 > 1" step="1">
                Información Crédito
              </v-stepper-step>

              <v-divider></v-divider>

              <v-stepper-step :complete="e1 > 2" step="2">
                Datos Empresariales
              </v-stepper-step>

              <v-divider></v-divider>

              <v-stepper-step step="3"> Crédito Pre Aprobado </v-stepper-step>
            </v-stepper-header>

            <v-stepper-items>
              <v-stepper-content step="1">
                <v-card>
                  <v-row>
                    <v-col>
                      <div
                        style="background-color: #004481; color: white"
                        class="pa-10"
                      >
                        <h1 align="center">{{ leftTitle }}</h1>
                        <br /><br />
                        <h2>{{ check1 }}</h2>
                        <br /><br />
                        <h2>{{ check2 }}</h2>
                        <br /><br />
                        <h2>{{ check3 }}</h2>
                      </div>
                    </v-col>
                    <v-col style="background: white">
                      <div class="pa-10">
                        <v-form ref="form" align="center">
                          <h1>
                            {{ rightTitle }}
                          </h1>
                          <br />
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.ruc"
                                  label="RUC / DNI"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-select
                                  v-model="form.reason"
                                  :items="items"
                                  :rules="[(v) => !!v || 'Item is required']"
                                  label="Motivo"
                                  required
                                  outlined
                                >
                                </v-select>
                              </div>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.email"
                                  :counter="max"
                                  :rules="rules"
                                  label="Email"
                                  outlined
                                  prepend-inner-icon="mdi-email"
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.phone"
                                  :counter="max"
                                  :rules="rules"
                                  label="Celular"
                                  outlined
                                  prepend-inner-icon="mdi-phone"
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <v-checkbox
                            v-model="ex4"
                            label="He leido y acepto la Politica de tratamiento de Proteccion de datos personales"
                            color="primary"
                            value="primary"
                            hide-details
                          ></v-checkbox>
                          <br /><br />
                          <v-btn
                            @click="e1 = 2"
                            color="secondary"
                            elevation="6"
                          >
                            Siguiente
                          </v-btn>
                        </v-form>
                      </div>
                    </v-col>
                  </v-row>
                </v-card>

                <!-- <v-btn color="primary" @click="e1 = 2"> Continue </v-btn>

                <v-btn text> Cancel </v-btn> -->
              </v-stepper-content>

              <v-stepper-content step="2">
                <v-card>
                  <v-row>
                    <v-col>
                      <div
                        style="background-color: white; color: white"
                        class="pa-10"
                      >
                        <v-form ref="form" align="center">
                          <v-col>
                            <div align="center">
                              <v-row>
                                <v-input>
                                  ¿Ud. es cliente del BBVA?

                                  <v-radio-group
                                    v-model="form.is_client"
                                    row
                                    class="pl-10"
                                  >
                                    <v-radio label="Si" value="si"></v-radio>
                                    <v-radio label="No" value="no"></v-radio>
                                  </v-radio-group>
                                </v-input>
                              </v-row>
                              <v-row v-if="form.is_client === 'si'">
                                <v-text-field
                                  v-model="form.seniority_company_years_number"
                                  label="¿Cuántos años lleva como cliente?"
                                  outlined
                                  placeholder="20"
                                >
                                </v-text-field>
                              </v-row>
                              <v-row v-if="form.is_client === 'si'">
                                <v-input>
                                  ¿Está afiliado de forma digital?
                                  <v-radio-group
                                    v-model="form.u_digital_affiliation_type"
                                    row
                                    class="pl-10"
                                  >
                                    <v-radio label="Si" value="1"></v-radio>
                                    <v-radio label="No" value="0"></v-radio>
                                  </v-radio-group>
                                </v-input>
                              </v-row>
                              <v-row
                                v-if="
                                  form.u_digital_affiliation_type === '1' &&
                                  form.is_client === 'si'
                                "
                              >
                                <v-input> ¿Desde cuando? </v-input>
                                <v-date-picker v-model="form.dias_digital">
                                </v-date-picker>
                              </v-row>
                              <v-row>
                                <v-text-field
                                  v-model="form.veh_ct"
                                  label="¿Cuántos vehículos posee?"
                                  outlined
                                  placeholder="3"
                                >
                                </v-text-field>
                              </v-row>
                              <v-row>
                                <v-text-field
                                  v-model="form.veh_year"
                                  label="¿De qué año es su vehículo más reciente?"
                                  outlined
                                  placeholder="2019"
                                >
                                </v-text-field>
                              </v-row>
                            </div>
                          </v-col>
                        </v-form>
                      </div>
                    </v-col>
                    <v-col style="background: white">
                      <div class="pa-10">
                        <v-form ref="form" align="center">
                          <label
                            >BBVA: Transferencias que planea realizar</label
                          >
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.traspaso_entre_ctes_ct"
                                  label="Cantidad"
                                  type="number"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.traspaso_entre_ctes_sm"
                                  label="Monto Total"
                                  type="number"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <label
                            >Otros Bancos: Transferencias que planea
                            realizar</label
                          >
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.trasf_env_ct"
                                  label="Cantidad"
                                  type="number"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.trasf_env_sm"
                                  label="Monto Total"
                                  type="number"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.employees_number"
                                  label="Número de empleados"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.monthly_income"
                                  label="Facturación Mensual Promedio"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.branches_number"
                                  label="Número de Sucursales, si es que la tiene"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.birth_date"
                                  label="Año de fundación de la empresa"
                                  placeholder="2020"
                                  outlined
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <br /><br />
                          <v-btn
                            @click="generateCredit"
                            color="secondary"
                            elevation="6"
                          >
                            Generar mi Crédito
                          </v-btn>
                        </v-form>
                      </div>
                    </v-col>
                  </v-row>
                </v-card>

                <!-- <v-btn color="primary" @click="e1 = 3">
                  Generar mi Crédito
                </v-btn>

                <v-btn text> Cancel </v-btn> -->
              </v-stepper-content>

              <v-stepper-content step="3">
                <v-card
                  class="mb-12"
                  color="grey lighten-1"
                  height="200px"
                ></v-card>

                <v-btn color="primary" @click="e1 = 1"> Continue </v-btn>

                <v-btn text> Cancel </v-btn>
              </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
        </v-col>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Simulador",
  data() {
    return {
      e1: 1,
      leftTitle: "Solicita tu crédito",
      check1: "Tu crédito disponible las 24 horas",
      check2: "Tu crédito a un solo paso",
      check3: "Solicita",
      rightTitle: "INGRESA TUS DATOS",
      items: ["Motivo 1", "Motivo 2", "Motivo 3", "Motivo 4"],
      date: null,
      form: {
        ruc: "",
        reason: "",
        email: "",
        phone: "",
        traspaso_entre_ctes_ct: 0,
        traspaso_entre_ctes_sm: 0,
        trasf_env_ct: 0,
        trasf_env_sm: 0,
        employees_number: 0,
        monthly_income: 0,
        branches_number: 0,
        // min_usd_billing_last_amount: 0, // Start of variables that have less cardinality and are guessed
        // max_usd_billing_last_amount: 0, // This and min shoulb be calculed based on their monthly income
        u_sms_affiliation_type: 0,
        traspaso_ctas_ct: 0,
        // traspaso_ctas_sm: 0,
        ranking_last_number: 0,
        dias_sms: 0,
        market_share_per: 0, //This should be considered based on shared market pbi
        pbi_sector_last_per: 0,
        trasf_rec_ct: 0,
        trasf_rec_sm: 0,
        min_pen_billing_last_amount: 0,
        // max_pen_billing_last_amount: 0, // These should be calculated based on their monthly income
        is_client: "",
        seniority_company_years_number: "",
        u_digital_affiliation_type: "",
        u_sms_affiliation_type: "",
        veh_ct: "",
        veh_year: "",
        birth_date: "",
      },
      url:
        "http://flask-env.eba-mp2pq4fm.us-east-1.elasticbeanstalk.com/api/predict",
      urlNode: "http://heroku.dev/whatever",
    };
  },
  methods: {
    generateCredit() {
      delete this.form["ruc"];
      delete this.form["reason"];
      delete this.form["email"];
      delete this.form["phone"];
      this.form["monthly_income"] = this.form["monthly_income"] / 500;
      delete this.form["is_client"];
      delete this.form["seniority_company_years_number"];

      let days = 0;
      this.form["dias_online"] = days; //////// This should be calculated reducing number of days
      this.form["dias_digital"] = days;
      this.form["u_sms_affiliation_type"] = this.form[
        "u_digital_affiliation_type"
      ];
      this.form["u_online_banking_affiliation_type"] = this.form[
        "u_digital_affiliation_type"
      ];

      //   console.log(this.form);

      axios
        .post(this.url, this.form)
        .then((result) => {
          this.e1 = 3;
          console.log("result", result);
        })
        .catch((error) => {
          console.log("error", error);
        });
    },
    saveUserData() {
      this.formUser["ruc"] = this.form["ruc"];
      this.formUser["reason"] = this.form["reason"];
      this.formUser["email"] = this.form["email"];
      this.formUser["phone"] = this.form["phone"];
      console.log("formUser", formUser);
      axios
        .post(this.urlNode, this.formUser)
        .then((result) => {
          this.e1 = 2; // We save data when we are on boarding.
          console.log("result node", result);
        })
        .catch((error) => {
          console.log("result node", error);
        });
    },
  },
};
</script>
