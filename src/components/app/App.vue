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
      isLoading: false
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
          return arr.filter(c => c.viewers > 100)
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
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=15')
        const newData = data.map(item => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 13,
        }))
        this.movies = newData
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false
      }
    },
  },
  mounted() {
    this.fetchMovie()
  },
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