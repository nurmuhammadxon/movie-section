<template>
  <div class="app">
    <div class="container">
      <AppInfo v-bind:allMoviesCount="movies.length"
        v-bind:favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <Box>
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </Box>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center text-2xl font-bold text-red-600">Kinolar yo'q</p>
      </Box>
      <Box v-else-if="isLoading" class="flex justify-center">
        <Loading />
      </Box>
      <MovieList v-else :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler"
        @onRemove="onRemoveHandler" />
      <Box class="flex items-center justify-center">
        <Pagination>
          <li v-for="pageNumber in totalPage" :key="pageNumber">
            <a href="#"
              class="flex items-center justify-center leading-tight px-3 h-8 border border-gray-300 transition-all"
              :class="[
                pageNumber === page
                  ? 'text-blue-600 bg-blue-50 hover:bg-blue-100 hover:text-blue-700'
                  : 'text-gray-500 bg-white  hover:bg-gray-100 hover:text-gray-700'
              ]" @click.prevent="goToPage(pageNumber)">
              {{ pageNumber }}
            </a>
          </li>
        </Pagination>
      </Box>
      <MoiveAddForm @creatMovie="creatMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from "../app-info/Appinfo.vue"
import SearchPanel from '../search-panel/SearchPanel.vue'
import AppFilter from '../app-fillter/AppFilter.vue'
import MovieList from '../movie-list/MovieList.vue'
import MoiveAddForm from '../movie-add-form/MoveAddForm.vue'
import axios from 'axios'

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MoiveAddForm,
  },
  data() {
    return {
      movies: [],
      term: '',
      filter: 'all',
      isLoading: false,
      limit: 10,
      page: 1,
      totalPage: 0,
    }
  },
  methods: {
    creatMovie(item) {
      item.id = this.movies.length + 1
      this.movies.push(item)
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] }
        }
        return item
      })
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(c => c.id !== id)
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr
      }
      term = term.toLowerCase()
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViewers':
          return arr.filter(c => c.viewers > 500)
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
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _limit: this.limit,
            _page: this.page,
          },
        })
        const newData = response.data.map(item => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 10,
        }))
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.movies = newData
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false
      }
    },
    goToPage(pageNumber) {
      this.page = pageNumber
    }
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

<style>
.app {
  height: 100vh;
  color: #000;
}

.container {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}
</style>