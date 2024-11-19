<script setup>
import { ref, computed } from "vue";

// Variables réactives pour les données de la carte
const cardNumber = ref("");
const cardHolderName = ref("");
const expiresMonth = ref("");
const expiresYear = ref("");
const cvv = ref("");

// Ajout espace tous les 4 chiffres
const formattedCardNumber = computed(() =>
  cardNumber.value.replace(/\s/g, "").replace(/(\d{4})(?=\d)/g, "$1 ")
);

const isCardNumberValid = computed(() => {
  return /^\d{16}$/.test(cardNumber.value); // Regex pour 16 chiffres
});

const addCard = () => {
  if (isCardNumberValid.value) {
    console.log("Card Number Added:", cardNumber.value);
    console.log("Cardholder Name:", cardHolderName.value);
    console.log("Expires Month", expiresMonth.value);
  } else {
    console.log("Numéro de card invalide");
  }
};
</script>

<template>
  <div class="flex items-center min-h-screen bg-gray-100 space-x-10">
    <!-- Formulaire de paiement -->
    <div class="p-6 bg-white rounded shadow-md">
      <h2 class="text-2xl font-bold mb-4">Add Payment Method</h2>

      <form @submit.prevent="addCard">
        <!-- Champ du numéro de carte -->
        <label class="block mb-2">Card Number</label>
        <input
          v-model="cardNumber"
          type="text"
          class="w-full p-2 mb-4 border rounded"
          placeholder="Enter your card number"
          maxlength="16"
        />

        <!-- Champ du nom du titulaire -->
        <label class="block mb-2">Cardholder Name</label>
        <input
          v-model="cardHolderName"
          type="text"
          class="w-full p-2 mb-4 border rounded"
          placeholder="Enter cardholder name"
        />
        <!-- Champ expiration du mois-->
        <label class="block mb-2">Expires Month</label>
        <input
          v-model="expiresMonth"
          type="text"
          class="w-16 p-2 mb-4 border rounded"
          placeholder="Month"
          maxlength="2"
        />
        <input
          v-model="expiresYear"
          type="text"
          class="w-16 p-2 mb-4 ml-2 border rounded"
          placeholder="Year"
          maxlength="2"
        />

        <input
          v-model="cvv"
          type="text"
          class="w-full p-2 mb-4 border rounded"
          placeholder="CVV"
          maxlength="3"
        />

        <button
          type="submit"
          :disabled="!isCardNumberValid"
          class="w-full p-2 bg-gradient-to-r from-blue-400 to-purple-600 text-white rounded"
        >
          Add Card
        </button>
      </form>
    </div>

    <!-- Visualisation de la carte -->
    <div
      class="p-6 bg-gradient-to-r from-blue-400 to-purple-600 text-white rounded-lg shadow-md w-80 h-48"
    >
      <div class="text-lg">
        {{ formattedCardNumber || "XXXX XXXX XXXX XXXX" }}
      </div>
      <div class="text-sm mt-4">CARDHOLDER</div>
      <div class="text-lg">{{ cardHolderName || "Cardholder Name" }}</div>

      <div class="text-sm mt-4">EXPIRES</div>
      <div class="text-lg">
        {{ expiresMonth ? expiresMonth + "/" + expiresYear : "MM/YY" }}
      </div>
    </div>
  </div>
</template>
