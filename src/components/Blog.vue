<template>
    <div>
        <button @click="emit('bigger')">+</button>
        <button @click="emit('smaller')">-</button>
<h2>Un titre d'un article </h2>
<p :style="{ fontSize: props.fontSize + 'px'}">The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested.</p>
    </div>
</template>

<script setup lang="ts">

    const props = defineProps<{
        fontSize:  number
    }>()

    const emit = defineEmits<{
        (e: 'bigger'): void
        (e: 'smallerr'): void

    }>()
       
    

</script>

<style scoped>

</style>