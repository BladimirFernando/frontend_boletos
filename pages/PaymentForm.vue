<!-- src/components/PaymentForm.vue -->
<template>
  <div>
    <stripe-form @submit="handleSubmit">
      <stripe-card ref="card" class="stripe-card" />
      <v-btn color="success" type="submit">
        Pagar
      </v-btn>
    </stripe-form>
  </div>
</template>

<script>
import { StripeForm, StripeCard } from 'vue-stripe-elements-plus'

export default {
  components: {
    'stripe-form': StripeForm,
    'stripe-card': StripeCard
  },
  props: {
    tour: {
      type: Object,
      required: true
    },
    userEmail: {
      type: String,
      required: true
    }
  },
  methods: {
    async handleSubmit (event) {
      event.preventDefault()
      try {
        const result = await this.$refs.card.createToken()
        if (result.error) {
          console.error(result.error.message)
        } else {
          this.$emit('paymentSuccess', result.token)
        }
      } catch (error) {
        console.error('Error:', error)
      }
    }
  }
}
</script>

  <style scoped>
  .stripe-card {
    margin-bottom: 20px;
  }
  </style>
