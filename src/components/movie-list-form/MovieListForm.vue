<template >
      <ul class="movie-list">
           <MovieListItem />
           <MovieListItem />
           <MovieListItem />
      </ul>
</template>

<script>
import MovieListItem from '../movie-list-utem/MovieListItem.vue';

export default {
    components: { MovieListItem }
}
</script>
<style >
      .movie-list{
              margin-bottom: 1rem;
  padding: 1rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
      }
</style>