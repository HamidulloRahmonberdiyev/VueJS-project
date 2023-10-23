<template>
    <div class="overflow-hidden rounded-lg border border-gray-200 shadow-md">
  <table class="w-full border-collapse bg-black text-left text-sm text-gray-500">
    <thead class="bg-white/5">
      <tr>
        <th scope="col" class="px-6 py-4 font-medium text-white">Film nomi</th>
        <th scope="col" class="px-6 py-4 font-medium text-white">Mamlakat</th>
        <th scope="col" class="px-6 py-4 font-medium text-white">Tomoshlar soni</th>
        <th scope="col" class="px-6 py-4 font-medium text-white">Amal</th>
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-100 border-t border-gray-100">
        <MovieListItem v-for="movie in movies"
          :movie="movie"
          :key="movie.id"
          @onToggle="$emit('onToggle', $event)"
          @onRemove="$emit('onRemove', movie.id)" />
    </tbody>
  </table>
</div>
</template>
<script>
import MovieListItem from '../movie-list-item/MovieListItem.vue';
export default {
    components: {MovieListItem},
    props: {
        movies: {
            type: Array,
            required: true,
        }
    }
}
</script>
<style></style>