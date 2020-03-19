<template>
  <div class="about flex flex-col items-center">
    <div class="absolute inset-0 z-0" @click="modal = false"></div>
    <input type="text" class="bg-gray-300 px-4 py-2 z-10" autocomplete="off" v-model="state"   @focus="modal = true">
    <div v-if="filteredStates && modal" class="z-10">
      <ul class="w-48 bg-gray-800 text-white">
        <li  class="py-2 border-b cursor-pointer" v-for="filteredState in filteredStates" :key="filteredState" @click="setState(filteredState)">{{filteredState}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      state: '',
      modal: false,
      states: [
        'Florida', 'Alabama', 'Alaska', 'Texas'
      ],
      filteredStates: [
      ],
    }
  },
  mounted(){
    this.filterStates();
  },
  watch: {
    state(){
      this.filterStates();
    }
  },
  methods: {
    filterStates(){
        if(this.state.length == 0){
          this.filteredStates = this.states;
        }
        this.filteredStates = this.states.filter(state => {
          return state.toLowerCase().startsWith(this.state.toLowerCase());
        })
    },
    setState(state){
      this.state = state;
      this.modal = false;
    }
  }
}
</script>
