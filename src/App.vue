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
        <div v-for="category in categories" :key="category.type" :class="category.class" v-show="productsByCategory[category.type].length">
          <productsList :categoryTitle="category.title" :categoryType="category.type" :products="filteredProductsByCategory(category.type)" @remove="removeProduct"/>
        </div>
      </div>
    </section>
  </main>
  <footerTemplate :remaining="remaining" :visibility="visibility" @clearCompletedProducts="clearCompletedProducts" :showOrNot="completedCount"/>
</template>


<script setup>
  import productsList from "./components/ProductsList.vue";
  import footerTemplate from "./components/footer.vue";
  import {ref, computed, onMounted, watch} from "vue";

  const filters = {
    all: (products) => products,
    active: (products) => products.filter((product) => !product.completed),
    completed: (products) => products.filter((product) => product.completed)
  };

  const visibility = ref('all');

  let productInput = ref('');
  let selectedType = ref('');
  const categories = [
  { title: 'Fruit & Vegetables', type: 'fruitsAndVegetables', class:'first-list' },
  { title: 'Meat', type: 'meat', class:'second-list' },
  { title: 'Dairy', type: 'dairy', class:'third-list' },
  { title: 'Pantry', type: 'pantry', class:'fourth-list' },
  { title: 'Home', type: 'home', class:'fifth-list' }
];
  const productsByCategory = ref({
    fruitsAndVegetables: [],
    meat: [],
    dairy:[],
    pantry:[],
    home:[],
  })
  const products = ref([])
  const remaining = computed(()=> products.value.filter((product)=>!product.completed).length)
  const completedCount = computed(()=>products.value.filter((product)=>product.completed).length)
  const saveProductsToLocalStorage = () => {
      localStorage.setItem('products', JSON.stringify(products.value));
  };


  const loadProductsFromLocalStorage = () => {
    const storedProducts = localStorage.getItem('products');
    if (storedProducts) {
      products.value = JSON.parse(storedProducts);
      products.value.forEach(product => {
        productsByCategory.value[product.type].push(product)
      })
    }
  };
  const onHashChange = ()=> {
      let hash = window.location.hash.replace(/#\/?/, '');
      if (filters[hash]) {
        visibility.value = hash;
      } else {
        window.location.hash = '';
        visibility.value = 'all';
      }
    };
  onMounted(()=>{
    loadProductsFromLocalStorage();
    window.addEventListener('hashchange', onHashChange);
    onHashChange();
  })

  watch(products, saveProductsToLocalStorage, { deep: true });

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
    productsByCategory.value[selectedType.value].push(newProduct)
    products.value.push(newProduct)
    productInput.value = '';
    selectedType.value = ''
    saveProductsToLocalStorage();
  }

  const removeProduct = (id) =>{
    products.value = products.value.filter((product) => product.id !== id)
    Object.keys(productsByCategory.value).forEach(category => {
      productsByCategory.value[category] = productsByCategory.value[category].filter(product => product.id !== id);
    })
  };
  const filteredProductsByCategory = (categoryType) => {
  return filters[visibility.value](products.value.filter(product => product.type === categoryType));
  };

  const clearCompletedProducts = (completed)=>{
    products.value = products.value.filter((product)=> !product.completed)
    Object.keys(productsByCategory.value).forEach(category => {
      productsByCategory.value[category] = productsByCategory.value[category].filter(product => !product.completed);
    })
  }
  
</script>