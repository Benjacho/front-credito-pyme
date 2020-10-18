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
                        style="background-color: #004481; color: white; height:100%"
                        class="pt-10"
                      >
                        <h1 align="center" class="pl-0">{{ leftTitle }}</h1>
                        <br /><br /><br>
                        <div class="pl-15">
                          <v-layout>
                            <p class="pr-5">
                              <v-img
                                class="pa-0 ma-0"
                                width="30"
                                src="https://d3n8a8pro7vhmx.cloudfront.net/afl/pages/2551/attachments/original/1429911676/white-checkmark-in-circle-md.png?1429911676"
                              ></v-img>
                            </p>
                            <h2>
                              {{ check1 }}
                            </h2>
                          </v-layout>
                          <br /><br />
                          <v-layout>
                            <p class="pr-5">
                              <v-img
                                class="pa-0 ma-0"
                                width="30"
                                src="https://d3n8a8pro7vhmx.cloudfront.net/afl/pages/2551/attachments/original/1429911676/white-checkmark-in-circle-md.png?1429911676"
                              ></v-img>
                            </p>
                            <h2>
                              {{ check2 }}
                            </h2>
                          </v-layout>
                          <br /><br />
                          <v-layout>
                            <p class="pr-5">
                              <v-img
                                class="pa-0 ma-0"
                                width="30"
                                src="https://d3n8a8pro7vhmx.cloudfront.net/afl/pages/2551/attachments/original/1429911676/white-checkmark-in-circle-md.png?1429911676"
                              ></v-img>
                            </p>
                            <h2>
                              {{ check3 }}
                            </h2>
                          </v-layout>
                        </div>
                      </div>
                    </v-col>
                    <v-col style="background: white">
                      <div class="pa-10">
                        <v-form ref="form" align="center" @submit.prevent="submit">
                          <h1 style="color: #004481">
                            {{ rightTitle }}
                          </h1>
                          <br />
                          <v-row>
                            <v-col>
                              <div style="p-5">
                                <v-text-field
                                  v-model="form.ruc"
                                  :rules="[rules.required]"
                                  label="RUC / DNI"
                                  outlined
                                  required
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                            <v-col>
                              <div style="p-5">
                                <v-select
                                  v-model="form.reason"
                                  :rules="[rules.required]"
                                  :items="items"
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
                                  :rules="[rules.required, rules.email]"
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
                                  :rules="[rules.required]"
                                  label="Celular"
                                  outlined
                                  prepend-inner-icon="mdi-phone"
                                >
                                </v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                          <v-checkbox
                            v-model="form.terms"
                            label="He leido y acepto la Politica de tratamiento de Proteccion de datos personales"
                            color="primary"
                            value="primary"
                            hide-details
                          ></v-checkbox>
                          <br /><br />
                          <v-btn
                            @click="e1 = 2"
                            :disabled="!form1IsValid"
                            color="secondary"
                            elevation="6"
                            type="submit"
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
                                  :rules="[rules.required]"
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
                                <v-date-picker 
                                  v-model="form.dias_digital"
                                  locale="pe"
                                >
                                </v-date-picker>
                              </v-row><br>
                              <v-row>
                                <v-text-field
                                  v-model="form.veh_ct"
                                  label="¿Cuántos vehículos posee?"
                                  outlined
                                  placeholder="3"
                                  :rules="[rules.required]"
                                  required
                                >
                                </v-text-field>
                              </v-row><br>
                              <v-row>
                                <v-text-field
                                  v-model="form.veh_year"
                                  label="¿De qué año es su vehículo más reciente?"
                                  outlined
                                  placeholder="2019"
                                  :rules="[rules.required, rules.veh_year]"
                                  required
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                                  :rules="[rules.required]"
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
                  class="mx-auto"
                  color="secondary"
                  width="600px"
                  style="color: white;"
                  elevation="24"
                  shaped
                >
                  <v-img
                    class="pa-0 ma-0"
                    height="250"
                    src="https://www.bbva.pe/content/dam/public-web/peru/photos/cards/card-productos-digitales-mayo.png.img.2400.1599837443512.png"
                  ></v-img>
                  <div
                    class="pa-15"
                  >
                  <v-card-text>
                    <h1>Detalles</h1><br>
                    <hr/><br><br>
                    <v-row>
                      <v-col>
                        <h2>{{Math.round(amount_prediction)}}</h2>
                        <label style="font-size: 14px;">Monto del préstamo</label><br><br>
                      </v-col>
                      <v-col>
                        <h2>{{Math.round(amount_prediction / 18)}}</h2>
                        <label style="font-size: 14px;">Cuota mensual</label>
                      </v-col>
                    </v-row>
                    <h3>29.34%</h3>
                    <label style="font-size: 14px;">Tasa de interés</label><br><br>
                    <h3>18 meses</h3>
                    <label style="font-size: 14px;">Plazo de financiamiento</label><br><br><br>
                    <p>
                      La empresa tiene la obligación de difundir información de conformidad con la Ley Nº 28587 y/o sus modificatorias.
                    </p>
                    <h3>INFORMACION REFERENCIAL</h3>
                    <p align="justify" class="pt-4">
                      Este simulador tiene carácter referencial, por lo tanto no es vinculante ni constituye declaración ni genera responsabilidad para el BBVA. Las cuotas del cronograma definitivo pueden variar respecto de las indicadas en este simulador en función a la aprobación crediticia, a las fechas de desembolso y al número de días considerados en el periodo de gracia.
                    </p><br>
                    <v-btn
                      elevation="3"
                      large
                      rounded
                    >
                      Ver Cronograma
                      <v-icon
                        right
                        dark
                      >
                        mdi-calendar
                      </v-icon>
                    </v-btn>
                  </v-card-text>
                  </div>
                </v-card>
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
        terms: false,
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
    rules: {
      required: value => !!value || 'Debe rellenar este campo.',
      ruc: [val => (val || '').length > 0 || 'Debe rellenar este campo'],
      email: value => {
        const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        return pattern.test(value) || 'E-mail inválido.'
      },
      veh_year: [val => (val || '').length < 4 || '4 digitos']
    },
	  amount_prediction: 0,
      url:
        "http://flask-env.eba-mp2pq4fm.us-east-1.elasticbeanstalk.com/api/predict",
      urlNode: "http://heroku.dev/whatever",
    };
  },

  computed: {
    form1IsValid () {
      return (
        this.form.ruc &&
        this.form.reason &&
        this.form.email &&
        this.form.phone &&
        this.form.terms
      )
    },
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
		  this.amount_prediction = result.data.predictions[0]
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
