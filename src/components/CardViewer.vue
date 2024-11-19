<script setup>
import { defineProps } from "vue";

// Définition des props
const props = defineProps({
  formattedCardNumber: {
    type: String,
    default: "XXXX XXXX XXXX XXXX",
  },
  expirationMonth: {
    type: String,
    default: "MM",
  },
  expirationYear: {
    type: String,
    default: "YY",
  },
});
</script>

<template>
  <div
    class="p-6 bg-gradient-to-r from-blue-400 to-purple-600 text-white rounded-lg shadow-md w-80 h-48"
  >
    <!-- Affichage du numéro de carte formaté -->
    <div class="text-lg">
      {{ props.formattedCardNumber || "XXXX XXXX XXXX XXXX" }}
    </div>
    <div class="text-sm mt-4">CARDHOLDER</div>
    <div class="text-lg">Cardholder Name</div>
    <div class="text-sm mt-4">EXPIRES</div>
    <div class="text-lg">
      {{ props.expirationMonth }}/{{ props.expirationYear }}
    </div>
  </div>
</template>

<style scoped>
/* Styles spécifiques */
</style>
