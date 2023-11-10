<template >
      <ul class="movie-list">
           <MovieListItem v-for="movie in movies" :movie="movie" :key="movie.id"
           @onToggle="$emit('onToggle', $event)"
           @onRemove="$emit('onRemove', movie.id)"/>
           
      </ul>
</template>

<script>
import MovieListItem from '../movie-list-utem/MovieListItem.vue';

export default {
    components: { MovieListItem },
    props:{
      movies:{
            type:Array,
            required:true,
      }
    }
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