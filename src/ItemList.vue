<script setup>
defineProps(['items','title']);

const importanceLabels = {
    high: 'High',
    medium: 'Medium',
    low: 'Low',
};

const importanceClasses = {
    high: 'is-danger',
    medium: 'is-warning',
    low: 'is-success',
};
</script>
<template>
    <h1>{{ title }}</h1>
    <ul>
        <li v-for="item in items" :key="item.id">
            {{ item.text }}
            <input type="checkbox" v-model="item.isDone">
        </li>
    </ul>
</template>