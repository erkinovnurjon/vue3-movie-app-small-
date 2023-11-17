<template >
  <Input  v-model="term"
      class=" search-input"
      placeholder="kinolarni qidirish"
      @input="changeHandler" />
      
</template>

<script>
import Input from '@/ui-component/Input.vue';

export default {
    props: {
        upDateTermHandler: {
            type: Function,
            required: true,
        },
    },
    data() {
        return {
            term: "",
        };
    },
    methods: {
        changeHandler(e) {
            this.term = e.target.value;
            this.upDateTermHandler(this.term);
        },
    },
    components: { Input }
}
</script>
<style scoped>
.search-input{
  margin-bottom: 1rem;
  padding: 1rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
}
      
</style>