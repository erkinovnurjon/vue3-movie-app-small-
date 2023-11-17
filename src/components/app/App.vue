<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter((c) => c.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel :upDateTermHandler="upDateTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center fs-3 text-danger">Kinolar yo'q</p>
      </Box>
      <Box v-else-if="isLoading" class="d-flex justify-content-center">
        <Loader />
      </Box>

      <MovieListForm
        v-else
        :movies="onFilterHandler(
          onSearchHandler(movies, term),
          filter
        )"
        @onToggle="onToggleHandler"
        @onRemove="onRemoveHandler"
      />
      <Box class="d-flex justify-content-center">
        <nav aria-label="pagination">
          <ul class="pagination pagination-sm">
            <li
              v-for="pageNumber in totalPages"
              :key="pageNumber"
              @click="changePage(pageNumber)"
              :class="{ active: pageNumber === page +1 }"
            >
              <span class="page-link">{{ pageNumber }}</span>
            </li>
          </ul>
        </nav>
      </Box>
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from "../app-info/AppInfo.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
import MovieListForm from "../movie-list-form/MovieListForm.vue";
import Loader from "@/ui-component/Loader.vue";
import axios from "axios";
import Box from "@/ui-component/Box.vue";

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieListForm,
    MovieAddForm,
    Box,
    Loader,
  },
  data() {
    return {
      movies: [],
      term: "",
      filter: "all",
      isLoading: false,
      limit: 10,
      page: 0,
      totalPages: 0,
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter((c) => c.id !== id);
    },
    upDateTermHandler(term) {
      this.term = term;
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr;
      }
      return arr.filter(
        (c) => c.name.toLowerCase().indexOf(term.toLowerCase()) > -1
      );
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 30);
        default:
          return arr;
      }
    },
    updateFilterHandler(filter) {
      this.filter = filter;
      this.page = 0; // Filtrlashda sahifani nolga sozlash
      this.fetchMovie(); // Filtrlashda ma'lumotlarni qayta yuklash
    },
    async fetchMovie() {
      try {
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _limit: this.limit,
              _page: this.page + 1, // Sahifa soni 1 dan boshlanadi
            },
          }
        );
        const newArr = response.data.map((item) => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 10,
        }));
        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.movies = newArr;
        this.isLoading = false;
      } catch (error) {
        console.error(error.message);
        this.isLoading = false;
      }
    },
    changePage(pageNumber) {
      this.page = pageNumber - 1; // Sahifani o'zgartirish
      this.fetchMovie(); // Ma'lumotlarni yangilash
    },
  },
  mounted() {
    this.fetchMovie();
  },
};
</script>

<style>
.app {
  height: 100vh;
  color: #000;
}
.content {
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
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
