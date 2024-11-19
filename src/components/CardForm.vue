<script setup>
import { ref, computed } from "vue";

// Déclaration de la variable cardNumber
const cardNumber = ref("");

// Formatage du numéro de carte en ajoutant des espaces tous les 4 chiffres
const formattedCardNumber = computed(() =>
  cardNumber.value.replace(/\s/g, "").replace(/(\d{4})(?=\d)/g, "$1 ")
);

// Vérifie si le numéro de carte a 16 chiffres et contient uniquement des chiffres
const isCardNumberValid = computed(() => {
  return /^\d{16}$/.test(cardNumber.value); // Regex pour 16 chiffres
});

const addCard = () => {
  if (isCardNumberValid.value) {
    console.log("Card Number Added:", cardNumber.value);
  } else {
    console.log("Invalid Card Number. It must be 16 digits.");
  }
};
</script>

<template>
  <div class="p-6 bg-white rounded shadow-md">
    <h2 class="text-2xl font-bold mb-4">Add Payment Method</h2>

    <form @submit.prevent="addCard">
      <label class="block mb-2">Card Number</label>
      <input
        v-model="cardNumber"
        type="text"
        maxlength="16"
        @input="cardNumber = cardNumber.replace(/[^0-9]/g, '').slice(0, 16)"
      />
      class="w-full p-2 mb-4 border rounded" placeholder="Enter your card
      number" required />

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
  <CardViewer :formattedCardNumber="formattedCardNumber" />
</template>

<style scoped>
/* Ajoute des styles si nécessaire */
</style>
