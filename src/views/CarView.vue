<script setup>
import { useRoute, RouterView, useRouter } from "vue-router";
import { ref, onBeforeMount } from "vue";
import carsData from "../data.json";
const route = useRoute();
const router = useRouter();
const car = ref(null);
const { id } = route.params;
onBeforeMount(() => {
  car.value = carsData.find((c) => c.id === parseInt(id));
});
</script>

<template>
  <div class="container">
    <div v-if="car">
      <h1>The Car</h1>
      <p>Make: {{ car.make }}</p>
      <p>Body: {{ car.body }}</p>
      <p>Price: ${{ car.price }}</p>
      <p>Year: {{ car.year }}</p>
      <RouterView />
      <button @click="router.back()">Go Back</button>
    </div>
    <div v-else>Car Not Found</div>
  </div>
</template>
