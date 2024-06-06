<template>
  <v-dialog v-model="dialog" max-width="500">
    <v-card class="payment-card">
      <v-card-title class="headline">
        Pago para {{ tour.origin }} - {{ tour.destination }}
      </v-card-title>
      <v-card-text>
        <div id="card-element" class="card-element" />
        <v-alert
          v-if="errorMessage"
          type="error"
          class="error-alert"
        >
          {{ errorMessage }}
        </v-alert>
      </v-card-text>
      <v-card-actions>
        <v-btn class="pay-button" color="success" @click="submitPayment">
          Pagar
        </v-btn>
        <v-btn class="cancel-button" @click="closeDialog">
          Cancelar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import { loadStripe } from '@stripe/stripe-js'

export default {
  props: {
    tour: Object
  },
  data () {
    return {
      dialog: true,
      stripe: null,
      elements: null,
      cardElement: null,
      clientSecret: '',
      errorMessage: ''
    }
  },
  async mounted () {
    this.stripe = await loadStripe(process.env.VUE_APP_STRIPE_PUBLIC_KEY)
    this.elements = this.stripe.elements()
    this.cardElement = this.elements.create('card')
    this.cardElement.mount('#card-element')
    this.createPaymentIntent()
  },
  methods: {
    async createPaymentIntent () {
      try {
        const response = await this.$axios.post('/create-payment-intent', {
          amount: this.tour.cost * 100 // Convert to cents
        })
        this.clientSecret = response.data.clientSecret
      } catch (error) {
        this.errorMessage = 'Failed to create payment intent'
      }
    },
    async submitPayment () {
      const { error, paymentIntent } = await this.stripe.confirmCardPayment(this.clientSecret, {
        payment_method: {
          card: this.cardElement
        }
      })
      if (error) {
        this.errorMessage = error.message
      } else {
        this.recordPayment(paymentIntent)
        this.$emit('payment-success')
      }
    },
    async recordPayment (paymentIntent) {
      try {
        await this.$axios.post('/record-payment', {
          tour: this.tour,
          paymentIntent
        })
      } catch (error) {
        console.error('Error recording payment:', error)
      }
    },
    closeDialog () {
      this.dialog = false
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
.payment-card {
  background-color: #f7f7f7;
  border-radius: 10px;
  padding: 20px;
}
.headline {
  font-size: 20px;
  font-weight: bold;
  color: #333;
}
.card-element {
  margin-bottom: 20px;
}
.error-alert {
  margin-bottom: 20px;
}
.pay-button {
  background-color: #4caf50 !important;
  color: #fff !important;
}
.cancel-button {
  color: #4caf50 !important;
}
</style>
