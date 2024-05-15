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
          <span class="barra">Inicio</span>
        </v-btn>
        <v-btn text class="black--text">
          <span class="barra">Beneficios</span>
        </v-btn>
        <v-btn text class="black--text">
          <span class="barra">Nosotros</span>
        </v-btn>
        <v-btn text class="black--text">
          <span class="barra">Ayuda</span>
        </v-btn>
        <v-btn style="background-color:lime; border-radius: 20px;">
          <span class="barra">Registrate gratis</span>
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-col>
          <p class="title" style="margin-left: 25px;">
            BENEFICIOS PARA MIEMBROS
          </p>
          <h3 class="h3-t" style="margin-left: 25px;">
            Crear una cuenta
          </h3>
          <p class="with-icon" style="margin-left: 25px;">
            Cancelaciones con un solo click *(Sujeto a términos y condiciones)
          </p>
          <p class="with-icon" style="margin-left: 25px;">
            Viajes gratis
          </p>
          <p class="with-icon" style="margin-left: 25px;">
            Tarifas especiales y promociones
          </p>
          <p class="with-icon" style="margin-left: 25px;">
            Seguro de viajero extendido
          </p>
          <p class="with-icon" style="margin-left: 25px;">
            Modificaciones a tu itinerario
          </p>
        </v-col>
        <v-row>
          <v-col>
            <v-img
              :src="require('../assets/images/playy.jpg')"
              height="90px"
              width="250px"
              alt="Descripción de la imagen"
              style="margin-left: 60px;"
            />
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="6" align="center" justify="center">
        <v-row>
          <v-col>
            <v-card color="white" class="custom-card">
              <v-card-text>
                <v-row>
                  <v-col>
                    <v-row>
                      <v-icon class="custom-icon mdi mdi-email-outline" style="margin-top: -25px;" />
                      <v-text-field v-model="email" label="Ingresa tu correo" outlined style="margin-left: 10px; font-family:'Roboto', sans-serif;" />
                    </v-row>
                  </v-col>
                </v-row>
                <v-row>
                  <v-icon class="custom-icon mdi mdi-lock" style="margin-top: -25px;" />
                  <v-text-field v-model="password" label="Ingresa tu contraseña" outlined type="password" style="margin-left: 10px;" />
                </v-row>
                <v-row align="center" style="margin-top: -20px;">
                  <v-col cols="auto">
                    <v-icon class="mdi mdi-help-circle-outline" style="margin-right: -20px;" />
                  </v-col>
                  <v-col cols="auto">
                    <span class="text-center">¿Olvidaste la contraseña?</span>
                  </v-col>
                </v-row>
              </v-card-text>
              <v-card-actions>
                <v-btn rounded align="center" justify="center" color="#33ffc7" @click="login">
                  <span class="barra" color: black justify="center">Iniciar sesión</span>
                </v-btn>
                <v-row class="rowCard" justify="center" />
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  // name: 'IndexPage',
  // auth: false
}
</script>

  <style>
  .custom-card {
    max-width: 300px;
    max-height: 300px;
    padding: 10px;
    font-size: 14px;
  }

  .barra {
    text-transform: none;
    font-size: 17px;
    font-family: 'Roboto', sans-serif;
    font-weight: bold;
  }

  .custom-icon {
    color: rgb(0, 0, 0) !important; /* Cambia "blue" al color deseado */
  }

  .with-icon::before {
    content: '\2714'; /* Código de carácter para el icono de check */
    color: green; /* Color del icono de check */
    margin-right: 5px; /* Espacio entre el icono y el texto */
  }

  .with-icon {
    font-family: 'Roboto', sans-serif; /* Cambia 'Roboto' por la fuente que desees */
  }

  .title {
    font-family: 'Roboto', sans-serif;
  }

  .h3-t {
    font-size: 40px;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  }

  </style>
