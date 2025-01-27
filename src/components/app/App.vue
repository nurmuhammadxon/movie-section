<template>
  <div class="app">
    <div class="container">
      <AppInfo />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList />
      <MoiveAddForm />
    </div>
  </div>
</template>

<script>
import AppInfo from "@/components/app-info/Appinfo.vue"
import SearchPanel from '@/components/search-panel/SearchPanel.vue'
import AppFilter from '../app-fillter/AppFilter.vue'
import MovieList from '../movie-list/MovieList.vue'
import MoiveAddForm from '../movie-add-form/MoiveAddForm.vue'

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MoiveAddForm,
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

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>