<template>
  <header class="header">
    <div class="header-container">
      <h1 class="header-title">Shopping List</h1>
      <form @submit.prevent="addProduct" class="input-container">
        <input v-model="productInput" class="header-input" type="text" name="mainInput" id="mainInput" placeholder="What do you want to buy today?">
        <select v-model="selectedType" name="" id="selectTypeOfProduct" required>
          <option value="" disabled selected>Select product type</option>
          <option v-for="category in categories" :key="category.type" :value="category.type">
            {{ category.title }}
          </option>
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
        <div v-for="category in categories" :key="category.type" :class="category.class">
          <productsList :categoryTitle="category.title" :categoryType="category.type" :products="products"/>
        </div>
        
        
        
      </div>
    </section>
  </main>
  <footerTemplate :remaining="remaining"/>
</template>


<script setup>
  import productsList from "./components/ProductsList.vue";
  import footerTemplate from "./components/footer.vue";
  import {ref, computed, onMounted} from "vue";

  let productInput = ref('');
  let selectedType = ref('');
  const categories = [
  { title: 'Fruit & Vegetables', type: 'fruitsAndVegetables', class:'first-list' },
  { title: 'Meat', type: 'meat', class:'second-list' },
  { title: 'Dairy', type: 'dairy', class:'third-list' },
  { title: 'Pantry', type: 'pantry', class:'fourth-list' },
  { title: 'Home', type: 'home', class:'fifth-list' }
];
  const products = ref([])
  const remaining = computed(()=>products.value.length)


  const addProduct = (e)=>{
    e.preventDefault();
    if (!productInput.value.trim() || !selectedType.value) {
      return;
    }
    const newProduct = {
      id:Date.now(),
      title: productInput.value.trim(),
      type: selectedType.value,
      completed: false,
    }
    products.value.push(newProduct)
    productInput.value = '';
    selectedType.value = ''
    saveProductsToLocalStorage();
  }

  const saveProductsToLocalStorage = () => {
    localStorage.setItem('products', JSON.stringify(products.value));
  };

  const loadProductsFromLocalStorage = () => {
    const storedProducts = localStorage.getItem('products');
    if (storedProducts) {
      products.value = JSON.parse(storedProducts);
    }
  };
  onMounted(()=>{
    loadProductsFromLocalStorage();
  })

</script>