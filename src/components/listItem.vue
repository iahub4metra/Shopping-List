<template>
    <li class="list-item">
        <input type="checkbox" name="checkbox-item" id="checkbox">
        <checkmarkIcon />
        <svg class="svg-icon">
            <use xlink:href="#icon-checkmark"></use>
        </svg>
        <p>{{title}}</p>
        <button type="button">X</button>
    </li>
</template>

<script setup>
import checkmarkIcon from './icons/checkmarkIcon.vue'
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
    title: String,
})





</script>