<template>
    <div class="w-full flex justify-between items-center p-3 mb-5">
        <h2 class="text-xl text-white font-semibold"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
            class="text-white w-8 h-8">
            <path stroke-linecap="round" stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
            </svg> Qidiruv ...
        </h2>
        <button id="openModalBtn" onclick="document.getElementById('myModal').showModal()" 
            class="flex items-center bg-yellow-400  border font-semibold py-2 px-4 rounded-md transition-colors duration-300">
            <svg class="w-4 h-4 mr-2 text-black" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
            </svg>
            <p class="text-black">Film qo'shish</p>
        </button>
    </div>
    <div class="w-full flex justify-center p-1 mb-5">
        <div class="relative w-full">
            <input type="text"
                class="w-full backdrop-blur-sm text-white bg-black/20 py-2 pl-10 pr-4 rounded-lg focus:outline-none border-2 border-gray-100 focus:border-yellow-300 transition-colors duration-300"
                placeholder="Qidiruv..." 
                :value="term" 
                @input="changeHandler">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                <svg class="w-4 h-4 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                    fill="none" viewBox="0 0 20 20">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                </svg>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        updateTermHandler: {
            type: Function,
            required: true,
        },
    },
    date() {
        return {
            term: '',
        }
    },
    methods: {
        changeHandler(e) {
            this.term = e.target.value
            this.updateTermHandler(this.term)
        },
    },
}
</script>
<style></style>