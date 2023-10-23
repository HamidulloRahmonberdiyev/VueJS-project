<template>
  <div class="bg-black flex items-center justify-center pt-10 pb-10 h-full">
    <div
      class="w-11/12 sm:w-11/12 md:w-8/12 lg:w-6/12 backdrop-blur-sm bg-white/10 p-6 rounded-lg shadow-sm border-yellow-200 border">
      <SearchPanel :updateTermHandler="updateTermHandler" />
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-2 gap-4 mb-5">
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
        <MovieAddform @createMovie="createMovie" />
      </div>
      <AppInfo :allMoviesCount="movies.length" />
      <Box v-if="!movies.length && !isLoading">
        <p class="text-red-600">Kinolar mavjud emas</p>
      </Box>
      <Box v-else-if="isLoading">
        <Loader />
      </Box>
      <MovieList v-else :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onLike="onToggleHandler"
        @onRemove="onRemoveHandler" />
      <Box>
        <nav aria-label="Page navigation example">
          <ul class="flex list-style-none">
            <li class="page-item" v-for="pageNumber in totalPages" :key="pageNumber"
              :class="{ 'rounded bg-blue-600': pageNumber == page }" @click="changePageHandler(pageNumber)">
              <a class="page-link relative block py-1.5 px-3 rounded border-0 outline-none transition-all duration-300 rounded text-white hover:text-white hover:bg-blue-600 shadow-md focus:shadow-md"
                href="#">{{ pageNumber }} <span class="visually-hidden"></span>
              </a>
            </li>
          </ul>
        </nav>
      </Box>
    </div>
  </div>
</template>

<script>
import AppInfo from '../app-info/AppInfo.vue';
import AppFilter from '../app-filter/AppFilter.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';
import MovieList from '../movie-list/MovieList.vue';
import MovieAddform from '../movie-add-form/MovieAddForm.vue';
import axios from 'axios'
export default {
  components: {
    AppInfo,
    AppFilter,
    SearchPanel,
    MovieList,
    MovieAddform,
  },
  data() {
    return {
      movies: [],
      term: '',
      filter: 'all',
      isLoading: false,
      limit: 10,
      page: 1,
      totalPages: 0,
    }
  },
  methods: {
    async createMovie(item) {
      try {
        const response = await axios.post('https://raw.githubusercontent.com/hjorturlarsen/IMDB-top-100/master/data/movies.json', item)
        this.movies.push(item)
      } catch (error) {
        alert(error.message())
      }
    },
    onToggleHandler(id, prop) {
      this.movies = this.movies.map(item => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] }
        }
        return item
      })
    },
    async onRemoveHandler(id) {
      try {
        const response = await axios.delete(`https://raw.githubusercontent.com/hjorturlarsen/IMDB-top-100/master/data/movies.json/${id}`)
        this.movies = this.movies.filter(c => c.id !== id)
        console.log(response)
      } catch (error) {
        alert(error.message)
      }
    },
    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViews':
          return arr.filter(c => c.show > 2000)
        case 'famous':
          return arr.filter(c => c.show > 1000)
        default:
          return arr
      }
    },
    updateTermHandler(term) {
      this.term = term
    },
    updateFilterHandler(filter) {
      this.filter = filter
    },
    async fetchMovie() {
      try {
        this.isLoading = true
        const response = await axios.get('https://raw.githubusercontent.com/hjorturlarsen/IMDB-top-100/master/data/movies.json', {
          params: {
            _limit: this.limit,
            _page: this.page,
          }
        })
        const newArr = response.data.map(item => ({
          id: item.id,
          name: item.title,
          country: 'Noma\'lum',
          show: item.rank ** 2 * 51,
          like: true,
        }))
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.movies = newArr
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false
      }
    },
    changePageHandler(page) {
      this.page = page
      this.fetchMovie()
    },
  },
  mounted() {
    this.fetchMovie()
  },
  watch: {
    page() {
      this.fetchMovie()
    }
  }
}

</script>

<style></style>