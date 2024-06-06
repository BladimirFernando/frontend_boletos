<template>
  <v-app>
    <v-container class="container-with-background">
      <v-row>
        <v-col v-for="tour in tours" :key="tour.id" cols="12" md="4">
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
              <v-btn rounded color="green" @click="showPaymentForm(tour)">
                Aceptar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <!-- Formulario de Pago -->
    <v-dialog v-model="showPayment" persistent max-width="600">
      <v-card>
        <v-card-title class="headline">
          Pago del Tour
        </v-card-title>
        <v-card-text>
          <v-form @submit.prevent="handlePayment">
            <!-- Campos adicionales para la información del pago -->
            <v-text-field
              v-model="userEmail"
              label="Email"
              required
            />
            <v-text-field
              v-model="cardNumber"
              label="Número de Tarjeta"
              required
            />
            <v-text-field
              v-model="expDate"
              label="Fecha de Vencimiento (MM/AA)"
              required
            />
            <v-text-field
              v-model="cvc"
              label="CVC"
              required
            />
            <v-btn type="submit" rounded color="green">
              Pagar
            </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      tours: [],
      showPayment: false,
      currentTour: null,
      userEmail: '',
      cardNumber: '',
      expDate: '',
      cvc: ''
    }
  },
  created () {
    const toursData = this.$route.query.tours
    if (toursData) {
      this.tours = JSON.parse(toursData)
    }
  },
  methods: {
    showPaymentForm (tour) {
      this.currentTour = tour
      this.showPayment = true
    },
    async handlePayment () {
      try {
        const response = await this.$axios.post('/payment', {
          userEmail: this.userEmail,
          tourId: this.currentTour.id,
          amount: this.currentTour.cost,
          // Agregar los campos adicionales al objeto de datos a enviar al servidor
          cardNumber: this.cardNumber,
          expDate: this.expDate,
          cvc: this.cvc
        })

        if (response.data.success) {
          alert('Pago exitoso')
          this.showPayment = false
        } else {
          alert('Pago fallido: ' + response.data.error)
        }
      } catch (error) {
        console.error('Error processing payment:', error)
        alert('Error procesando el pago')
      }
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
  background-color: #030000; /* Color de fondo de las tarjetas */
  border: 2px solid #ccc; /* Borde de las tarjetas */
  border-radius: 10px; /* Bordes redondeados de las tarjetas */
  margin-bottom: 20px; /* Espacio entre tarjetas */
}

.headline {
  font-size: 20px;
  font-weight: bold;
}

/* Estilos para los botones */
.v-btn {
  color: white !important;
}

/* Estilos para el botón de Aceptar */
.accept-btn {
  background-color: #008060 !important; /* Color de fondo del botón */
}

/* Estilos para el botón de Pagar */
.pay-btn {
  background-color: #ff6347 !important; /* Color de fondo del botón */
}

/* Estilos para el botón de Cerrar */
.close-btn {
  background-color: #ccc !important; /* Color de fondo del botón */
}
</style>
