<template >
      <Box  @submit.prevent>
          <h3>Yangi kino qo'shish</h3>
          <form class="add-form d-flex">
            <Input class="new-movie-label"  placeholder="Qanday kino?" v-model="name" />
            <Input class="new-movie-label" placeholder="Nechi marotaba ko'rilgan?" v-model="viewers" type="number" />
          
           
            <PrimaryButton class=" btn-outline-dark" @click="addMovie">
                Qo'shish
            </PrimaryButton>
          </form>
      </Box>
</template>
<script>
import PrimaryButton from '@/ui-component/PrimaryButton.vue'
import Box from '../../ui-component/Box.vue'
import Input from '../../ui-component/Input.vue'

export default {
    data(){
        return{
            name:'',
            viewers:'',
        }
    },
    components:{
    PrimaryButton,
    Box,
    Input
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