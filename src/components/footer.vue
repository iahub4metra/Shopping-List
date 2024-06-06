<template>
    <footer>
        <span class="wrap-span">
            <p>{{num}}</p>
            <span>
                <p>items left</p>
            </span>
        </span>
        <div class="footer-container">
            <ul>
                <li><a class="footer-link" href="#/all">All</a></li>
                <li><a class="footer-link" href="#/active">Active</a></li>
                <li><a class="footer-link" href="#/completed">Completed</a></li>
            </ul>
            <button @click="increment" type="button">Clear completed</button>
        </div>
    </footer>
</template>


<script setup>
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
    num: Number,
})
const emit = defineEmits(['increment'])
const increment = ()=>{
    emit("increment")
}
</script>