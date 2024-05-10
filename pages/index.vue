<template>
  <v-container fluid>
    <v-row>
      <v-col>
        <v-img
          :src="require('../assets/images/connectando.jpg')"
          height="120px"
          width="120px"
          alt="Descripción de la imagen"
          style="margin-left: 60px;"
        />
      </v-col>
      <v-col>
        <v-btn text class="black--text">
          Inicio
        </v-btn>
        <v-btn text class="black--text">
          Acerca de
        </v-btn>
        <v-btn text class="black--text">
          Contacto
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card rounded color="white" class="custom-card" style="margin-left: 800px;">
          <v-card-text>
            <v-row>
              <v-text-field v-model="email" label="Ingresa tu correo" outlined />
            </v-row>
            <v-row>
              <v-text-field v-model="password" label="Ingresa tu contraseña" outlined type="password" />
            </v-row>
          </v-card-text>
          <v-card-actions>
            <v-btn block class="pa-2" color="#33ffc7" @click="login">
              <span style="text-transform: none; color: white;">Iniciar sesión</span>
            </v-btn>
            <v-row class="rowCard" justify="center" />
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
  }
}
</script>

<style>
.custom-card {
  max-width: 300px; /* Establecer el ancho máximo del v-card */
  max-height: 300px; /* Establecer la altura máxima del v-card */
  padding: 10px; /* Reducir el padding interno del v-card */
  font-size: 14px; /* Reducir el tamaño de la fuente dentro del v-card */
}
</style>
