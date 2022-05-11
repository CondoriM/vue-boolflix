<template>
  <div id="app" class="bg-secondary">
    <HeadSite v-model="searchT" @formSubmit="state"></HeadSite>

    <div class="container-fluid">
      <div class="row">
        <div class="col text-center">
          <MovieComp class="m-2" :film="film" v-for="(film,index) in films" :key="index"></MovieComp>
          <SerieComp :serie="serie" v-for="serie in series" :key="serie.id"></SerieComp>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import vText from "@/state"
import HeadSite from "@/components/HeadComponent.vue"
import MovieComp from "@/components/MovieComponent.vue"
import SerieComp from "@/components/SerieComponent.vue"

export default {
  name: 'App',
  components: {
    MovieComp,
    SerieComp,
    HeadSite
  },

  data(){
    return{
      searchT: '',
      films: [],
      series: [],
      flags: '',
    
      apy_key: '626f23522e216489e48887e2688ac97f',
    }
  },

  methods:{
    state(){
      console.log('ricerca');
      vText.searchT = this.searchT
      this.searchAll()
      this.searchT = ''
    },

    searchAll(){
      this.searchFilms()
      this.searchSeries()
      this.flag()
    },

    searchFilms(){
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apy_key}&language=it-IT&page=1&include_adult=false&query=${this.searchT}`).then(response =>{
      this.films = response.data.results
      this.films.forEach(film => {
        film.vote_average = Math.floor(film.vote_average / 2) 
      });
      })
    },

    searchSeries(){
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apy_key}&language=it_IT&query=${this.searchT}`).then(response =>{
      this.series = response.data.results
      this.series.forEach(serie => {
        serie.vote_average = Math.floor(serie.vote_average / 2)
      });
      })
    },

    flag(){
      axios.get(`https://flagcdn.com/it/codes.json`).then(response =>{
      this.flags = response.data
      //console.log(this.flags,'ciao');
      })
    },

    star(f){
      if (f.vote_average <= 1 && f.vote_average != 0) {
        return 4
      }if(f.vote_average > 1 && f.vote_average <= 2){
        return 3
      }if(f.vote_average > 2 && f.vote_average <= 3){
        return 2
      }if(f.vote_average > 3 && f.vote_average <= 4){
        return 1
      }if(f.vote_average > 4 && f.vote_average <= 5){
        return 0
      }if(f.vote_average == 0){
        return 5
      }
    }
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
