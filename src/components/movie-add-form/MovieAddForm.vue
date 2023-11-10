<template >
      <div class="movie-add-form" @submit.prevent>
          <h3>Yangi kino qo'shish</h3>
          <form class="add-form d-flex">
            <input type="text" class="form-control new-movie-label" placeholder="Qanday kino?" :value="name" @input="name = $event.target.value">
            <input type="text" class="form-control new-movie-label" placeholder="Nechi marotaba ko'rilgan?" :value="viewers" @input="viewers = $event.target.value">
            <button class="btn btn-outline-dark" @click="addMovie">
                Qo'shish
            </button>
          </form>
      </div>
</template>
<script>
export default {
    data(){
        return{
            name:'',
            viewers:'',
        }
    },
    methods:{
        addMovie(){
            if(!this.name || !this.viewers) return
                const newMovie = {
                name:this.name,
                viewers:this.viewers,
                like:false,
                favourite:false,
                id:Date.now()
            }
            this.$emit('createMovie' , newMovie)
            this.name="",
            this.viewers=""
        }
    }
    
    
      
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