<template>
  <div id="app">
    <HeadSite/>
    <form @submit.prevent="search">
      <input type="text" v-model="searchT">
      <button type="submit">Invia</button>
      <div v-for="(film,index) in films" :key="index">
        {{film.original_title}}
      </div>
    </form>
    
    {{searchT}}
  </div>
</template>

<script>
import axios from "axios";
import HeadSite from '@/components/HeadComponent.vue'

export default {
  name: 'App',
  components: {
    HeadSite
  },

  data(){
    return{
      searchT: '',
      films: '',
      apy_key: '626f23522e216489e48887e2688ac97f',
    }
  },

  methods:{
    search(){
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apy_key}&language=it-IT&page=1&include_adult=false&query=${this.searchT}`).then(response =>{
      this.films = response.data.results
      console.log(this);
      console.log(this.films);
    })
    }
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
