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
      },
      url:
        "http://flask-env.eba-mp2pq4fm.us-east-1.elasticbeanstalk.com/api/predict",
    };
  },
  methods: {
    generateCredit() {
	  this.url = "http://127.0.0.1:5000/api/predict"; //override for now
	  delete this.form['ruc']
	  delete this.form['reason']
	  delete this.form['email']
	  delete this.form['phone']
      axios
        .post(this.url, this.form)
        .then((result) => {
          console.log(result);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
