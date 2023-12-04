<script setup>

defineProps(['inicio','fin','maxLength']);
const emit = defineEmits(['next', 'prev'])

</script>

<template>
    <div class="btn-group me-2" role="group" aria-label="Basic example">
        <button @click="$emit('prev')" 
        type="button" class="btn btn-outline-primary" 
        :disabled="inicio <= 0">Previus</button>&nbsp;

        <button @click="$emit('next')" 
        type="button" class="btn btn-outline-primary" 
        :disabled="fin >= maxLength">Next</button>
        <!-- <button type="button" class="btn btn-primary">Right</button> -->
    </div>
</template>
