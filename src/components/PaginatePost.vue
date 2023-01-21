<script setup>

const emit = defineEmits(['nextPag', 'previusPag'])

const props = defineProps({
    activeNext: Boolean,
    activePrevius: Boolean
})


</script>

<template>

    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-outline-primary" @click="emit('previusPag')" :disabled="activePrevius">Previus</button>
        <button type="button" class="btn btn-outline-primary" @click="emit('nextPag')" :disabled="activeNext">Next</button>
    </div>


</template>