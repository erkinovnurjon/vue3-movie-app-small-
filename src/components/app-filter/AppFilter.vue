<template >
      <div class="btn-group">
            <button class="btn btn-dark " type="button" @click="filterHandler('all')">
                 Barcha kinolar
            </button>
            <button class="btn btn-outline-dark " type="button" @click="filterHandler('favourite')">
                 Mashhur kinolar kinolar
            </button>
            <button class="btn btn-outline-dark " type="button" @click="filterHandler('mostViewers')">
                 Eng ko'p ko'rilganlar
            </button>
      </div>
</template>

<script>
export default {
     props:{
          updateFilterHandler:{
               type:Function,
               required :true
          }
     },
     data() {
          return {
               filter:'all'
          }
     },
     methods: {
          filterHandler(filter){
               this.filter = filter
               this.updateFilterHandler(this.filter)
          }
     },
      
}
</script>

<style >
      
</style>