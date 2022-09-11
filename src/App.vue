<template>
  <Blog @bigger="add" @smaller="less" :fontSize="fontSize"/>
  <br/>
  <Product :voiture="voiture" />
  <br />
  <button @click="toogle = !toogle">toogle</button>
  <br />
  <div v-if="toogle">
    <br />
    <h2 @click="changeName">Bonjour {{ user.name }} - {{ user.age }} ans</h2>
    <br />
    <h2>Count{{ count }}</h2>
    <br />

    <div>
      <button @click="incremente">add</button>
      <button @click="decremente">less</button>
    </div>
    <h2>Prix total Ht :{{ totalPriceHt }}</h2>
    <h2>Prix total TTC :{{ totalPricettc }}</h2>
    <input type="number" v-model="product.quantity" />
    <input type="number" v-model="price" />
    <br />
    <input v-model="letter" type="text" />

    <h1 v-if="letter === 'A'">A</h1>
    <h1 v-else-if="letter === 'B'">B</h1>
    <h1 v-else-if="letter === 'C'">C</h1>
    <h1 v-else-if="letter === 'D'">D</h1>
    <h1 v-else>Autre</h1>

    titre du text : {{ text }}

    <input
      class="input"
      :class="{
        inputOngoing,
        inputError,
        inputValid,
      }"
      @focus="
        input.focus = true;
        input.touched = true;
      "
      @blur="input.focus = false"
      type="text"
      v-model="input.value"
    />
  </div>

  <ul>
    <li v-for="({ name, notes, sex }, index) of users">
      {{ index }}-{{ name }},{{ sex }}, notes:
      <span v-for="note in notes">{{ note }}</span>
    </li>
  </ul>
</template>

<script setup lang="ts">
import Product from "./components/Product.vue";
import Blog from "./components/Blog.vue";
import type { Voiture } from "@/interfaces/voiture.interface";

import { computed, ref, watch, reactive ,onMounted} from "vue";
const toogle = ref(false);

const text = ref("");
const price = ref(0);
const letter = ref("");
const fontSize = ref(36)

const input = reactive({
  value: "",
  focus: false,
  touched: false,
});
const voiture = reactive<Voiture>({
  name: "Porche",
  prix: 100000,
  available: true,
});
const users = reactive([
  { name: "oiive", sex: "masculin", notes: [4, 5, 7] },
  { name: "seb", sex: "masculin", notes: [4, 7, 7] },
  { name: "karine", sex: "feminin", notes: [9, 5, 7] },
]);

const inputOngoing = computed(() => input.focus && input.value.length);
const inputError = computed(
  () => !input.focus && input.touched && input.value.length < 5
);
const inputValid = computed(
  () => input.touched && !input.focus && !inputError.value
);

const state = reactive({
  user: {
    name: "olive",
    age: 43,
    isActive: false,
  },
  product: {
    name: "books",
    quantity: 3,
    priceHt: 10,
    nbrOfModification: 0,
  },
});


const totalPriceHt = computed(() => product.priceHt * product.quantity);
const totalPricettc = computed(() => product.priceHt * product.quantity * 1.2);

watch([() => state.product.quantity, price], (newValue, oldValue) => {
  state.product.nbrOfModification++;
  console.log(state.product);
});
const { user, product } = state;

const count = ref(0);

function incremente() {
  count.value++;
}
function decremente() {
  count.value--;
}
function changeName() {
  user.name = user.isActive ? "olive" : "seb";
  user.isActive = !user.isActive;
}

function add(){
  fontSize.value++
}
function less(){
  fontSize.value--
}

setTimeout(() => {
  user.name = "Paul";
}, 3000);
</script>

<style scoped>
.input {
  outline: 0;
  border: 2px solid black;
  border-radius: 4px;
}
.inputOngoing {
  border-color: blue;
}
.inputError {
  border-color: red;
}
.inputValid {
  border-color: green;
}
</style>
