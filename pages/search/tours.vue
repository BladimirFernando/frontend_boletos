<template>
  <v-app>
    <v-container class="container-with-background">
      <v-row>
        <v-col
          v-for="tour in tours"
          :key="tour.id"
          cols="12"
          md="4"
        >
          <v-card class="tour-card" outlined>
            <v-card-title class="headline">
              {{ tour.origin }} - {{ tour.destination }}
            </v-card-title>
            <v-card-subtitle>
              Fecha de Ida: {{ tour.departureDate }}<br>
              Fecha de Regreso: {{ tour.returnDate }}<br>
              Hora de salida: {{ tour.departureTime }}<br>
              Hora de llegada: {{ tour.returnTime }}<br>
              Duracion: {{ tour.duration }}<br>
              Pasajeros: {{ tour.passengers }}<br>
              Precio: ${{ tour.cost }}
            </v-card-subtitle>
            <v-card-actions>
              <v-spacer />
              <v-btn rounded color="green" @click="acceptTour(tour)">
                Aceptar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      tours: []
    }
  },
  created () {
    // Parse tours data from query parameters
    const toursData = this.$route.query.tours
    if (toursData) {
      this.tours = JSON.parse(toursData)
    }
  },
  methods: {
    acceptTour (tour) {
      console.log('Tour accepted:', tour)
      // Aquí puedes agregar la lógica para aceptar el tour
    }
  }
}
</script>

  <style scoped>
  .container-with-background {
    background: url('assets/images/verde.jpg') no-repeat center center fixed;
    background-size: cover;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .tour-card {
    background-color: black !important;
  }
  .headline {
    font-size: 24px;
    font-weight: bold;
    color: white
  }
  .v-btn {
    background-color: #008060 !important; /* Color verde agua llamativo */
    color: white !important;
  }
  </style>
