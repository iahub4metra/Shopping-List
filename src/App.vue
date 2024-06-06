<template>
  <header class="header">
    <div class="header-container">
      <h1 class="header-title">Shopping List</h1>
      <form @submit.prevent="addProduct" class="input-container">
        <input v-model="productInput" class="header-input" type="text" name="mainInput" id="mainInput" placeholder="What do you want to buy today?">
        <select v-model="selectedType" name="" id="selectTypeOfProduct" required>
          <option value="" disabled selected>Select product type</option>
          <option value="fruitsAndVegetables">Fruit & Vegetables</option>
          <option value="meat"> Meat</option>
          <option value="dairy">Dairy</option>
          <option value="pantry">Pantry</option>
          <option value="home">Home</option>
        </select>
        <button class="btn-sub">Add</button>
      </form>
    </div>
    <ol class="decorative-list">
      <li class="decorative-list-item">
        <p>Buy it with thought</p>
      </li>
      <li class="decorative-list-item">
        <p>Cook it with care</p>
      </li>
      <li class="decorative-list-item">
        <p>Eat it with love</p>
      </li>
    </ol>
  </header>
  <main>
    <section>
      <div class="parent">
        <div class="first-list">
          <h2 class="list-title">Fruit & Vegetables</h2>
          <ul>
            <listItem 
              v-for="product in filteredProducts('fruitsAndVegetables')"
              :key="product.id"
              :title="product.title"
            />
          </ul>
        </div>
        <div class="second-list">
          <h2 class="list-title">Meat</h2>
          <ul>
            <listItem 
              v-for="product in filteredProducts('meat')"
              :key="product.id"
              :title="product.title"
            />
          </ul>
        </div>
        <div class="third-list">
          <h2 class="list-title">Dairy</h2>
          <ul>
            <listItem
              v-for="product in filteredProducts('dairy')"
              :key="product.id"
              :title="product.title"
            />
          </ul>
        </div>
        <div class="fourth-list">
          <h2 class="list-title">Pantry</h2>
          <ul>
            <listItem
              v-for="product in filteredProducts('pantry')"
              :key="product.id"
              :title="product.title"
            />
          </ul>
        </div>
        <div class="fifth-list">
          <h2 class="list-title">Home</h2>
          <ul>
            <listItem
              v-for="product in filteredProducts('home')"
              :key="product.id"
              :title="product.title"
            />
          </ul>
        </div>
      </div>
    </section>
  </main>
  <footerTemplate :remaining="remaining"/>
</template>


<script setup>
import listItem from "./components/listItem.vue";
import footerTemplate from "./components/footer.vue";
import {ref, computed} from "vue";

let productInput = ref('');
let selectedType = ref('');

const products = ref([])
const remaining = computed(()=>products.value.length)


const addProduct = (e)=>{
  e.preventDefault();
  if (!productInput.value.trim() || !selectedType.value) {
    return;
  }
  products.value.push({
    id:Date.now(),
    title: productInput.value.trim(),
    type: selectedType.value,
    completed: false,
  })
  productInput.value = '';
  selectedType.value = ''
}

const filteredProducts = (type) => {
  return products.value.filter(product => product.type === type);
}

</script>