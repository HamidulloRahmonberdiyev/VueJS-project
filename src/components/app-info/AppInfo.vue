<template>
    <Box>
        <h3 class="pr-20 font-mono">Filmlar soni: {{ allMoviesCount }}</h3>
    </Box>
</template>

<script>
export default {
    props: {
        allMoviesCount: {
            type: Number,
            required: true,
        },
    },
}
</script>

<style></style>