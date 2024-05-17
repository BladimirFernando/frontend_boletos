<template>
  <v-container fill-height>
    <v-row
      align="center"
      justify="center"
    >
      <v-col cols="12" md="6" lg="4">
        <v-card class="pa-4" max-width="400" elevation="4">
          <v-card-title class="headline">
            Bienvenido
          </v-card-title>
          <b style="font-family: 'Roboto', sans-serif;  font-weight: bold; margin-left: 17px;">
            A donde viajaremos hoy?
          </b>
          <v-card-actions>
            <v-btn color="primary">
              Acción 1
            </v-btn>
            <v-btn color="secondary">
              Acción 2
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  auth: true
}
</script>

<style scoped>
html, body, #__nuxt, #__layout {
  height: 100%;
}

.headline {
  font-weight: bold;
  font-family: 'Roboto', sans-serif;
}

.custom-card {
  border-radius: 100px; /* Ajusta este valor según sea necesario */
}
</style>
