<template>
    <button class="backdrop-blur-sm bg-black/80 p-6 rounded-md shadow-sm cursor-pointer border-2 border-gray-50 hover:border-violet-200 hover:border-2 transition-colors duration-300">
        <slot></slot>
    </button>
</template>
<script>
export default {
    name: 'FilterButton'
}
</script>
<style>
    
</style>