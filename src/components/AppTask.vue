<script setup>
import { ref } from "vue";

const textInput = ref("");
const result = ref(null);
const error = ref("");

function handleSearch() {
  error.value = "";
  result.value = null;

  const numbers = textInput.value
    .split(",")
    .map((num) => parseInt(num.trim()))
    .filter((num) => !isNaN(num));

  //console.log("tablica liczb:", numbers);

  if (numbers.length < 3) {
    error.value = "Podaj co najmniej 3 liczby rozdzielone przecinkami.";
    return;
  }

  result.value = findNumber(numbers);
}

function findNumber(arr) {
  const even = arr.filter((num) => num % 2 === 0);
  const odd = arr.filter((num) => num % 2 !== 0);

  return even.length === 1 ? even[0] : odd[0];
}
</script>

<template>
  <div class="container">
    <div class="card">
      <input type="text" v-model="textInput" placeholder="2,4,0,100,4,11..." />
      <button @click="handleSearch">Wyszukaj</button>
      <p v-if="error" class="error">{{ error }}</p>
    </div>

    <div class="arrow">→</div>

    <div class="card result-card">
      <div class="display-number">
        {{ result !== null ? result : "?" }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  height: 100vh;
}

.card {
  width: 250px;
  height: 350px;
  border: 1px solid black;
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  background-color: #ffffff;
}

.display-number {
  font-size: 48px;
  font-weight: bold;
  margin-top: 50px;
}

.arrow {
  font-size: 40px;
  font-weight: bold;
}

input {
  width: 90%;
  padding: 8px;
  margin: 20px 0;
}

button {
  padding: 10px 20px;
  cursor: pointer;
  border: 1px solid #000;
}

.error {
  margin-top: 20px;
  color: red;
  font-size: 12px;
  text-align: center;
}
</style>
