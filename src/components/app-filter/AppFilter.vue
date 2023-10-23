<template>
    <FilterButton v-for="btn in filterButton" :key="btn.name"
        :class="[filterName == btn.name ? 'bg-black/60' : '']"
        @click="filterHandler(btn.name)">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
            class="w-10 h-10 text-yellow-500">
            <path stroke-linecap="round"
                d="M15.75 10.5l4.72-4.72a.75.75 0 011.28.53v11.38a.75.75 0 01-1.28.53l-4.72-4.72M4.5 18.75h9a2.25 2.25 0 002.25-2.25v-9a2.25 2.25 0 00-2.25-2.25h-9A2.25 2.25 0 002.25 7.5v9a2.25 2.25 0 002.25 2.25z" />
        </svg>
        <h2 class="text-xl text-white font-semibold mb-4">{{ btn.title }}</h2>
        <p class="text-gray-400">Uzbek tilidagi eng sara ommabop filmlar</p>
    </FilterButton>
</template>

<script>
export default {
    props: {
        updateFilterHandler: {
            type: Function,
            required: true,
        },
        filterName: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            filterButton: [
                {
                    title: 'Barcha filmlar',
                    name: 'all',
                },
                {
                    title: 'Eng ko\'p tomosha qilingan',
                    name: 'mostViews',
                },
                {
                    title: 'Sevimli',
                    name: 'popular',
                },
                {
                    title: 'Mashhur',
                    name: 'famous',
                }
            ],
            filter: 'all'
        }
    },
    methods: {
        filterHandler(filter) {
            this.filter = filter
            this.updateFilterHandler(this.filter)
        },
    },
}
</script>

<style></style>