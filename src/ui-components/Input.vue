<template>
    <input type="text" :value="modelValue" @input="updateInput" class="w-full backdrop-blur-sm bg-black/50 text-white py-2 pl-10 m-2 pr-4 rounded-lg focus:outline-none border-2 border-white  transition-colors duration-300">
</template>
<script>
export default {
    name: 'Input',
    props: {
        modelValue: [String, Number],
    },
    methods: {
        updateInput(e) {
            this.$emit('update:modelValue', e.target.value)
        }
    },
}
</script>
<style>
    
</style>