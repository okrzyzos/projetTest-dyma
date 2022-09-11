<template>
  <div>
    <h2>La voiture de sport est la marque {{ title }} et son prix est de {{voiture.prix}} €</h2>
  </div>
</template>

<script setup lang="ts">
import type { Voiture } from "@/interfaces/voiture.interface";

import { computed } from "vue";
const props = defineProps<{
  voiture: Voiture;
}>();

const title = computed(() => props.voiture.name.toUpperCase());
</script>

<style scoped></style>
