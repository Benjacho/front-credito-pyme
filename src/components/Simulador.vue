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
                                <v-row >
                                    <v-input>
                                    ¿Ud. es cliente del BBVA?
                                    
                                    <v-radio-group
                                      v-model="form.is_client"
                                      row
                                      class="pl-10"
                                    >
                                      <v-radio
                                        label="Si"
                                        value="si"
                                      ></v-radio>
                                      <v-radio
                                        label="No"
                                        value="no"
                                      ></v-radio>
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
                                    <v-radio
                                      label="Si"
                                      value="si"
                                    ></v-radio>
                                    <v-radio
                                      label="No"
                                      value="no"
                                    ></v-radio>
                                  </v-radio-group>
                                  </v-input>
                                </v-row>
                                <v-row v-if="form.u_digital_affiliation_type === 'si' && form.is_client === 'si'">
                                  <v-input>
                                    ¿Desde cuando?
                                  </v-input>
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

                <v-btn color="primary" @click="e1 = 3"> Continue </v-btn>

                <v-btn text> Cancel </v-btn>
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
        is_client: "",
        seniority_company_years_number: "",
        u_digital_affiliation_type: "",
        dias_digital: "",
        veh_ct: "",
        veh_year: "",
      },
    };
  },
};
</script>
