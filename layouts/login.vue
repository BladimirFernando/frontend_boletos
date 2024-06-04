<template>
  <v-app style="background-color: white!important;">
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
          <v-btn style="background-color:lime; border-radius: 20px;" @click="showDialog = true">
            <span class="barra">Registrate gratis</span>
          </v-btn>
        </v-col>
      </v-row>
      <v-dialog v-model="showDialog" persistent width="500" transition="dialog-bottom-transition">
        <v-card>
          <v-card-title>Registro de Nuevo Usuario</v-card-title>
          <v-card-text>
            <v-text-field v-model="username" label="Nombre de usuario" style="color: white !important;" />
            <v-text-field v-model="registerEmail" label="Correo electrónico" />
            <v-text-field v-model="registerPassword" label="Contraseña" type="password" />
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn style="color: aqua;" @click="register">
              Registrar
            </v-btn>
            <v-btn color="red" @click="showDialog = false">
              Cancelar
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-row>
        <v-col cols="6">
          <v-col>
            <p class="title" style="margin-left: 25px; color: black;">
              BENEFICIOS PARA MIEMBROS
            </p>
            <h3 class="h3-t" style="margin-left: 25px; color: black;">
              Crear una cuenta
            </h3>
            <p class="with-icon" style="margin-left: 25px; color: black;">
              Cancelaciones con un solo click *(Sujeto a términos y condiciones)
            </p>
            <p class="with-icon" style="margin-left: 25px; color: black;">
              Viajes gratis
            </p>
            <p class="with-icon" style="margin-left: 25px; color: black;">
              Tarifas especiales y promociones
            </p>
            <p class="with-icon" style="margin-left: 25px; color: black;">
              Seguro de viajero extendido
            </p>
            <p class="with-icon" style="margin-left: 25px; color: black;">
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
                        <v-text-field v-model="email" label="Ingresa tu correo" outlined style="margin-left: 10px; font-family:'Roboto', sans-serif;" class="black-text-field" />
                      </v-row>
                    </v-col>
                  </v-row>
                  <v-row>
                    <v-icon class="custom-icon mdi mdi-lock" style="margin-top: -25px;" />
                    <v-text-field
                      v-model="password"
                      label="Ingresa tu contraseña"
                      outlined
                      type="password"
                      style="margin-left: 10px;"
                      class="black-text-field"
                    />
                  </v-row>
                  <v-row align="center" style="margin-top: -20px;">
                    <v-col cols="auto">
                      <v-icon class="custom-icon mdi mdi-help-circle-outline" style="margin-right: -20px;" />
                    </v-col>
                    <v-col cols="auto">
                      <span class="text-center" style="color:darkgray;">¿Olvidaste la contraseña?</span>
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
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      email: null,
      password: null,
      username: null,
      registerEmail: null,
      registerPassword: null,
      showDialog: false
    }
  },
  methods: {
    login () {
      console.log('@@@ datos', this.email, this.password)
      const sendData = {
        email: this.email,
        password: this.password
      }
      this.$auth.loginWith('local', {
        data: sendData
      }).then((res) => {
        const result = res.data
        if (result.message === 'success') {
          this.$store.commit('setToken', result.token)
          this.$router.push('/principal')
        }
      }).catch((err) => {
        console.log('@@@ error=> ', err)
      })
    },
    register () {
      const url = '/register'
      const data = {
        email: this.registerEmail,
        password: this.registerPassword,
        username: this.username
      }
      this.$axios.post(url, data)
        .then((res) => {
          console.log(res)
          if (res.data.message === 'User registered successfully') {
            this.showDialog = false
          }
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
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
  color: rgb(0, 0, 0) !important;
}

.with-icon::before {
  content: '\2714';
  color: green;
  margin-right: 5px;
}

.with-icon {
  font-family: 'Roboto', sans-serif;
}

.title {
  font-family: 'Roboto', sans-serif;
}

.h3-t {
  font-size: 40px;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}

.black-text-field input {
  color: black !important;
}

.v-application--is-ltr .v-label {
  color: black !important;
}
</style>email: this.registerEmailusername: this.username
