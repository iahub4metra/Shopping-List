<template>
    <footer>
        <span class="wrap-span">
            <p>{{ remaining}}</p>
            <span>
                <p>{{remaining === 1 ? 'item' : 'items'}} left</p>
            </span>
        </span>
        <div class="footer-container">
            <ul>
                <li><a class="footer-link" href="#/all">All</a></li>
                <li><a class="footer-link" href="#/active">Active</a></li>
                <li><a class="footer-link" href="#/completed">Completed</a></li>
            </ul>
            <button type="button">Clear completed</button>
        </div>
    </footer>
</template>


<script setup>
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
    remaining: Number,
})
</script>