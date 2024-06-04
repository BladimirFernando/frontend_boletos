<template>
  <v-app>
    <v-container class="container-with-background">
      <v-card class="mx-auto white-background" max-width="800">
        <v-card-title>
          <span class="headline black-text">Buscar Viajes</span>
        </v-card-title>
        <v-card-text class="black-text" style="font-family: 'Roboto', sans-serif; font-weight: bold;">
          A donde viajaremos hoy?
        </v-card-text>
        <v-card-text>
          <v-form>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  v-model="formData.origin"
                  label="Origen"
                  outlined
                  dense
                  class="black-text-field"
                />
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  v-model="formData.destination"
                  label="Destino"
                  outlined
                  dense
                  class="black-text-field"
                />
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-menu
                  v-model="menuDeparture"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  :return-value.sync="formData.departureDate"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template #activator="{ on, attrs }">
                    <v-text-field
                      v-model="formData.departureDate"
                      label="Fecha de Ida"
                      prepend-icon="mdi-calendar"
                      v-bind="attrs"
                      outlined
                      type="date"
                      dense
                      class="black-text-field"
                      v-on="on"
                    />
                  </template>
                  <v-date-picker
                    v-model="formData.departureDate"
                    no-title
                    scrollable
                    @input="menuDeparture = false"
                  />
                </v-menu>
              </v-col>
              <v-col cols="12" sm="6">
                <v-menu
                  v-model="menuReturn"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  :return-value.sync="formData.returnDate"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template #activator="{ on, attrs }">
                    <v-text-field
                      v-model="formData.returnDate"
                      label="Fecha de Regreso"
                      prepend-icon="mdi-calendar"
                      v-bind="attrs"
                      outlined
                      type="date"
                      dense
                      class="black-text-field"
                      v-on="on"
                    />
                  </template>
                  <v-date-picker
                    v-model="formData.returnDate"
                    no-title
                    scrollable
                    @input="menuReturn = false"
                  />
                </v-menu>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  v-model="formData.passengers"
                  label="Número de Usuarios"
                  type="number"
                  outlined
                  dense
                  class="black-text-field"
                />
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn rounded align="center" justify="center" color="#33ffc7" @click="searchTrips">
            Buscar Tours
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      menuDeparture: false,
      menuReturn: false,
      formData: {
        origin: '',
        destination: '',
        departureDate: '',
        returnDate: '',
        passengers: 1
      }
    }
  },
  methods: {
    async searchTrips () {
      try {
        const response = await this.$axios.get(`/tours?origin=${this.formData.origin}`)
        this.$router.push({
          path: '/search/tours',
          query: { tours: JSON.stringify(response.data) }
        })
      } catch (error) {
        console.error('Error fetching tours:', error)
      }
    }
  }
}
</script>

<style scoped>
.headline {
  font-size: 24px;
  font-weight: bold;
}
.container-with-background {
  background: url('assets/images/verde.jpg') no-repeat center center fixed;
  background-size: cover;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.white-background {
  background-color: white !important;
}
.black-text-field .v-input__control .v-input__slot input {
  color: black !important;
}
.black-text-field .v-label {
  color: black !important;
}
.black-text {
  color: black !important;
}
</style>
