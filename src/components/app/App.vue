<template>
  <div class="app">
    <div class="container">
      <AppInfo v-bind:allMoviesCount="movies.length"
        v-bind:favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <Box>
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </Box>
      <MovieList :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler"
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
      movies: [
        {
          name: "Qashqirlar makoni",
          viewers: 811,
          favourite: false,
          like: true,
          id: 1,
        },
        {
          name: "Forsaj",
          viewers: 462,
          favourite: false,
          like: false,
          id: 2,
        },
        {
          name: "Yangi o'rgimchak odam",
          viewers: 643,
          favourite: true,
          like: false,
          id: 3,
        },
      ],
      term: '',
      filter: 'all'
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