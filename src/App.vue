<script setup>
import { computed, ref } from 'vue';
import ItemList from './src/ItemList.vue/index.js';

let i = 0;
let message = ref('');
let items = ref(
    {id: i++, text: 'Apple', isDone: false},
    {id: i++, text: 'Pineapple', isDone: false},
    {id: i++, text: 'Grape', isDone: false},
    {id: i++, text: 'Green Apple', isDone: false}
);

function add (){
    if (message.value.trim() !== ''){
        items.value.push({id: i++, text: message, isDone: false});
    }
    message.value = '';
}

let doneItems = computed(() => items.value.filter(item => item.isDone));
let toDoItems = computed(() => items.value.filter(item => !item.isDone));
</script>

<template>
    <div class="container content mt-2">
        <div class="control is-expanded">
            <input @keydown.enter="add" v-model="message" class="input" type="text" placeholder="Add Item">
        </div>
        <div class="control">
            <button @click="add" class="button is-info">
                Add
            </button>
        </div>

        <ItemList :items="items" title="All Items"></ItemList>
        <ItemList :items="doneItems" title="Done Items"></ItemList>
        <ItemList :items="toDoItems" title="TODO"></ItemList>
    </div>
</template>