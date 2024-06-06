<template>
  <header class="header">
    <div class="header-container">
      <h1 class="header-title">Shopping List</h1>
      <form action="" class="input-container">
        <input class="header-input" type="text" name="mainInput" id="mainInput" placeholder="What do you want to buy today?" required>
        <select name="" id="selectTypeOfProduct" required>
          <option value="" disabled selected>Select product type</option>
          <option value="fruitsAndVegetables">Fruit & Vegetables</option>
          <option value="meat"> Meat</option>
          <option value="dairy">Dairy</option>
          <option value="pantry">Pantry</option>
          <option value="home">Home</option>
        </select>
        <button type="submit" class="btn-sub">Add</button>
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
            <listItem/>
          </ul>
        </div>
        <div class="second-list">
          <h2 class="list-title">Meat</h2>
          <ul>
            <listItem/>
          </ul>
        </div>
        <div class="third-list">
          <h2 class="list-title">Dairy</h2>
          <ul>
            <listItem/>
          </ul>
        </div>
        <div class="fourth-list">
          <h2 class="list-title">Pantry</h2>
          <ul>
            <listItem/>
          </ul>
        </div>
        <div class="fifth-list">
          <h2 class="list-title">Home</h2>
          <ul>
            <listItem/>
          </ul>
        </div>
      </div>
    </section>
  </main>
  <footerTemplate :num="counts.count" @increment="incrementParent"/>
</template>


<script setup>
import listItem from "./components/listItem.vue";
import footerTemplate from "./components/footer.vue";
import {ref} from "vue";

const counts = ref({
  count:0,
})
const incrementParent = ()=>{
  counts.value.count++
}



</script>