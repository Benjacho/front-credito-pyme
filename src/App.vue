<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center pl-5">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2 pb-4"
          contain
          src="https://www.bbva.pe/content/dam/public-web/global/images/logos/logo_bbva_blanco.svg"
          transition="scale-transition"
          width="150"
        />

        <!--<v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />-->
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
      </v-btn>
    </v-app-bar>

    <v-main>
      <Simulador />
    </v-main>
  </v-app>
</template>

<script>
import Simulador from "./components/Simulador";

export default {
  name: "App",

  components: {
    Simulador,
  },

  data: () => ({
    //
  }),
};
</script>
