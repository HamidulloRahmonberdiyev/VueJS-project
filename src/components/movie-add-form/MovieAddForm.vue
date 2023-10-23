<template>
    <dialog id="myModal" class="h-auto w-11/12 md:w-1/2 p-5 bg-black/90 rounded-md ">
        <div class="bg-black">
            <div class="flex flex-col w-full h-auto bg-white/10 rounded-lg shadow-sm border-yellow-200 border">
                <!-- Header -->
                <div class="flex w-full h-auto justify-center items-center">
                    <div class="flex w-10/12 h-auto py-3 justify-center text-white items-center text-2xl font-bold">
                        Film qo'shish
                    </div>
                    <div onclick="document.getElementById('myModal').close();"
                        class="flex w-1/12 h-auto justify-center text-white cursor-pointer">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="w-6 h-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </div>
                    <!--Header End-->
                </div>
                <!-- Modal Content-->
                <form @submit.prevent>
                    <div
                        class="flex w-full h-auto py-10 px-3 justify-center items-center bg-white/10 rounded text-center text-gray-500">
                        <Input 
                            v-model="name" 
                            placeholder="Nomi" />
                    </div>
                    <div
                        class="flex w-full h-auto px-3 justify-center items-center bg-white/10 rounded text-center text-gray-500">
                        <Input 
                            v-model="country"
                            placeholder="Davlati" />
                    </div>
                    <div
                        class="flex w-full h-auto px-3 py-10 justify-center items-center bg-white/10 rounded text-center text-gray-500">
                        <Input 
                             v-model="show"
                            placeholder="Tomoshalar soni" />
                    </div>
                    <PrimaryButton @click="addMovie">
                        <p class="text-black">Saqlash</p>
                    </PrimaryButton>
                </form>
                <!-- End of Modal Content-->
            </div>
        </div>
    </dialog>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            country: '',
            show: '',
        }
    },
    methods: {
        addMovie() {
            if (!this.name)
                return
            const newMovie = {
                name: this.name,
                country: this.country,
                show: this.show,
            }
            this.$emit('createMovie', newMovie)
            this.name = '',
                this.country = '',
                this.show = ''
        }
    }
}
</script>

<style></style>