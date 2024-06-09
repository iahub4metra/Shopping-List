<template>
    <footer>
        <span class="wrap-span">
            <p>{{ remaining}}</p>
            <span>
                <p>{{remaining === 1 ? 'product' : 'products'}} left</p>
            </span>
        </span>
        <transition name="fade">
            <div class="footer-container" v-if="showOrNot > 0">
            <ul>
                <li><a class="footer-link" href="#/all" :class="{ selected: visibility === 'all'}" >All</a></li>
                <li><a class="footer-link" href="#/active" :class="{ selected: visibility === 'active' }" >Active</a></li>
                    <li>
                        <a 
                        class="footer-link" 
                        href="#/completed" 
                        :class="{ selected: visibility === 'completed'}" 
                        >Completed
                        </a>
                    </li>
            </ul>
                <button @click="clearCompletedProducts" type="button">Clear completed</button>
        </div>
        </transition>
        
    </footer>
</template>


<script setup>
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
    remaining: Number,
    visibility: String,
    showOrNot: Number,
});
const emit = defineEmits(['clearCompletedProducts'])
const clearCompletedProducts = ()=>{
    emit('clearCompletedProducts')
}
</script>

<style scoped>
    .fade-enter-active, .fade-leave-active{
        transition: transform 1000ms cubic-bezier(0.4, 0, 0.2, 1);
    }
    .fade-enter-from, .fade-leave-to{
        transform: translateX(130%);
    }
</style>