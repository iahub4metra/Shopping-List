<template>
        <h2 class="list-title">{{categoryTitle}}</h2>
        <ul>
            <li v-for="product in filteredProducts(categoryType)" :key="product.id" class="list-item">
                <input type="checkbox" name="checkbox-item" id="checkbox">
                <checkmarkIcon />
                <svg class="svg-icon">
                    <use xlink:href="#icon-checkmark"></use>
                </svg>
                <p>{{product.title}}</p>
                <button @click="remove(product.id)" type="button">X</button>
            </li>
        </ul>
</template>

<script setup>
import checkmarkIcon from './icons/checkmarkIcon.vue'
import { defineProps, defineEmits, computed } from 'vue';
const props = defineProps({
    categoryTitle: String,
    categoryType:String,
    products: Array,
})
const emit = defineEmits(['remove'])
const remove = (id)=>{
    emit('remove', id)
}
const filteredProducts = (type) => {
    return props.products.filter(product => product.type === props.categoryType);
  }
</script>