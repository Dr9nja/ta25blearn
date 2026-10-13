<script setup>
import { computed, ref } from 'vue';
import ItemList from './ItemList.vue';

let i = 1;
let message = ref('');
let importance = ref('medium');
let items = ref([
    {id: i++, text: 'Apple', isDone: false},
    {id: i++, text: 'Pineapple', isDone: true},
    {id: i++, text: 'Grape', isDone: false},
    {id: i++, text: 'Green Apple', isDone: true},
]);

const importanceOrder = {high: 3, medium: 2, low: 1};

function sortByImportance(list) {
  return [...list].sort((a, b) => importanceOrder[b.importance] - importanceOrder[a.importance]);
}

function add(){
  if(message.value.trim() !== ''){
    items.value.push({id: i++, text: message.value.trim(), isDone: false});
  }
  message.value = '';
}

let doneItems = computed(() => items.value.filter(item => item.isDone));
let toDoItems = computed(() => items.value.filter(item => !item.isDone));
</script>

<template>
    <div class="container content mt-2">
        <div class="field has-addons">
            <div class="control is-expanded">
                <input @keydown.enter="add" v-model="message" class="input" type="text" placeholder="Add item">
            </div>
            <div class="control">
                <button @click="add" class="button is-info">
                    Add
                </button>
            </div>
        </div>
        
        <ItemList :items="items" title="All Items"></ItemList>
        <ItemList :items="doneItems" title="Done Items"></ItemList>
        <ItemList :items="toDoItems" title="TODO"></ItemList>
    </div>
</template>

<style></style>