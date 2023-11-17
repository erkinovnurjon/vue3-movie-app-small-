<template>
  <div class="btn-group">
    <PrimaryButton
      v-for="btn in filterButtons"
      :key="btn.name"
      
      :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark']"
      @click="filterHandler(btn.name)"
    >
      {{ btn.title }}
    </PrimaryButton>
  </div>
</template>

<script>
import PrimaryButton from '@/ui-component/PrimaryButton.vue';

export default {
    props: {
        updateFilterHandler: {
            type: Function,
            required: true
        },
        filterName: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            filterButtons: [
                {
                    title: "Barcha kinolar",
                    name: "all"
                },
                {
                    title: "Mashhur kinolar",
                    name: "popular"
                },
                {
                    title: "Eng ko'p ko'rilganlar",
                    name: "mostViewers"
                },
            ],
            filter: "all"
        };
    },
    methods: {
        filterHandler(filter) {
            this.filter = filter;
            this.updateFilterHandler(this.filter);
        }
    },
    components: { 
     PrimaryButton,
 },
};
</script>

<style>

</style>


 