<script setup>
defineEmits(['custom-toggle'])

</script>


<template>
    <button class="button" @click="$emit('custom-toggle')" >
        <slot/>

    </button>

  
</template>