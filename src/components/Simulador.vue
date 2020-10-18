<template>
    <div>
        <v-container
            class="grey lighten-5 pa-0"
            fluid
        >
        <v-layout
            
            no-gutters
            style="height: 300px"
        >
            <v-col>
                <div
                    style="background-color: #004481; color: white"
                    class="pa-10"  
                >
                    <h1 align="center">{{leftTitle}}</h1>
                    <br><br>
                    <h2>{{check1}}</h2>
                    <br><br>
                    <h2>{{check2}}</h2>
                    <br><br>
                    <h2>{{check3}}</h2>
                </div>
            </v-col>
            <v-col>
                <div
                    class="pa-10"
                >
                    <v-form ref="form" align="center">
                        
                        <h1 >
                            {{rightTitle}}
                        </h1>
                        <br>
                            <v-row>
                                <v-col>
                                    <div
                                        style="p-5"
                                    >
                                        <v-text-field                                           
                                            v-model="rfc"
                                            label="RUC / DNI"
                                            outlined                                            
                                        >   
                                        </v-text-field>
                                    </div>
                                </v-col>  
                                <v-col>
                                    <div
                                        style="p-5"
                                    >
                                        <v-select
                                            v-model="motivo"
                                            :items="items"
                                            :rules="[v => !!v || 'Item is required']"
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
                                    <div
                                        style="p-5"
                                    >
                                        <v-text-field
                                            v-model="email"
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
                                    <div
                                        style="p-5"
                                    >
                                        <v-text-field
                                            v-model="celular"
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
                        <br><br>
                        <v-btn
                            color="secondary"
                            elevation="6"
                        >
                            Siguiente
                        </v-btn> 
                    </v-form>
                </div>
            </v-col>
        </v-layout>
        </v-container>
    </div>
</template>

<script>
  export default {
    name: 'Simulador',

    data() {
        return {
            leftTitle: 'Solicita tu credito',
            check1: 'Tu credito disponible las 24 horas',
            check2: 'Tu credito a un solo paso',
            check3: 'Solicita',
            rightTitle: 'INGRESA TUS DATOS',
            items: [
                'Motivo 1',
                'Motivo 2',
                'Motivo 3',
                'Motivo 4',
            ],
        }    
    }
  }
</script>
