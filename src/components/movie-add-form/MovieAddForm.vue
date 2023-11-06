<template >
      <div class="movie-add-form">
          <h3>Yangi kino qo'shish</h3>
          <form class="add-form d-flex">
            <input type="text" class="form-control new-movie-label" placeholder="Qanday kino?">
            <input type="text" class="form-control new-movie-label" placeholder="Nechi marotaba ko'rilgan?">
            <button class="btn btn-outline-dark">
                Qo'shish
            </button>
          </form>
      </div>
</template>
<script>
export default {
      
}
</script>
<style >
      .movie-add-form{
  margin-bottom: 1rem;
  padding: 1rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
      }
</style>