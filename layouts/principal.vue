<template>
  <v-container fill-height>
    <v-row
      align="center"
      justify="center"
    >
      <v-col cols="12" md="6" lg="4">
        <v-card class="pa-4" max-width="400">
          <v-card-title class="headline">
            Título de la Tarjeta
          </v-card-title>
          <v-card-text>
            Este es un ejemplo de una tarjeta centrada en la pantalla usando Vuetify.
          </v-card-text>
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
}
</script>

  <style scoped>
  html, body, #__nuxt, #__layout {
    height: 100%;
  }
  </style>
