<template>
  <div class="app font-monospace">
    <div class="content ">

      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter((c) => (c.favourite)).length" />
      <div class="search-panel">
         <SearchPanel />
         <AppFilter />
      </div>
      <MovieListForm :movies="movies" @onToggle="onToggleHandler"  />
      <MovieAddForm  @createMovie="createMovie" />
    </div>
    
  </div>

</template>

<script>
  import AppInfo from "../app-info/AppInfo.vue";
  import AppFilter from "../app-filter/AppFilter.vue"
  import SearchPanel from "../search-panel/SearchPanel.vue"
  import  MovieAddForm from "../movie-add-form/MovieAddForm.vue"
  import MovieListForm  from "../movie-list-form/MovieListForm.vue"
export default {
  components : {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieListForm,
    MovieAddForm,

  },
  data(){
      return{
            movies:[
                  {
                        name:"Omar ",
                        viewers:811,
                        favourite:true,
                        like:true,
                        id:1,
                  },
                  {
                        name:"Empire of USman ",
                        viewers:746,
                        favourite:false,
                        like:false,
                        id:2,
                  },
                  {
                        name:"Ertugrul ",
                        viewers:689,
                        favourite:false,
                        like:false,
                        id:3,
                  },
            ]
      }
    },
    methods:{
      createMovie(item){
        this.movies.push(item)
      },
      onToggleHandler({id,prop}){
        this.movies = this.movies.map((item) => {
          if(item.id == id){
            return {...item , [prop]: !item[prop]}
          }
          return item
        })
      },
      
    },
}


</script>

<style>
.app{
  height: 100vh;
  color: #000;
}
.content{
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}
.search-panel{
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
}


</style>