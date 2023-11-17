<template >
      <input type="text" class="form-control" :value="modelValue" @input="updateInput">
      
</template>

<script>

export default {
     methods: {
      updateInput(e){
            this.$emit('update:modelValue' , e.target.value)
      }
     }, 
     props :{
      modelValue :[String , Number]
     }
}
</script>
<style scoped>
      
</style>