<script setup>
defineProps(['items','title']);

const importanceLabels = {
    high: '!!!',
    medium: '!!',
    low: '!',
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
        <li v-for="item in items" :key="item.id" :class="`priority-${item.importance}`">
            {{ item.text }}
            <span class="item-meta">
                <span class="tag" :class="importanceClasses[item.importance]">
                    {{ importanceLabels[item.importance] }}
                </span>
                <input type="checkbox" v-model="item.isDone" :aria-label="`Mark ${item.text} as done`">
            </span>
        </li>
    </ul>
</template>