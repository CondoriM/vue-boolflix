<template>
  <div id="app">
    <HeadSite/>
    <form @submit.prevent="searchAll">
      <input type="text" v-model="searchT">
      <button type="submit">Invia</button>
      <div class="container">
        <div class="row">
          <div class="col-2 flex-column" v-for="(film,index) in films" :key="index">
            <div class="col">
              <img class="img-fluid" :src="cover+film.poster_path" alt="">
            </div>

            <div class="stars">
                <font-awesome-icon v-for="(star,index) in film.vote_average" :key="index" icon="fa-solid fa-star" />
                <font-awesome-icon v-for="(star,index) in film.vote_average" :key="index" icon="fa-solid fa-star" />
            </div>

            <div class="col">
              {{film.original_title}}
              {{film.title}}
              <div>
                {{film.original_language}} 
                <img :src="'https://flagcdn.com/w20/'+ film.original_language +'.png'" alt="">
              </div>
              {{film.vote_average}}
            </div>
          </div>

          <div class="col-2 flex-column" v-for="serie in series" :key="serie.id">
            <div class="col">
              <img class="img-fluid" :src="cover+serie.poster_path" alt="">
            </div>

            <div class="stars">
                <font-awesome-icon v-for="(star,index) in serie.vote_average" :key="index" icon="fa-solid fa-star" />
            </div>

            <div class="col">
              {{serie.name}}
              <div>
                {{serie.original_language}} 
                <img :src="'https://flagcdn.com/w20/'+ serie.original_language +'.png'" alt="">
              </div>
              {{serie.vote_average}}
            </div>
          </div>
        </div>
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
      films: [],
      series: [],
      flags: '',

      cover: 'https://image.tmdb.org/t/p/w342',
      apy_key: '626f23522e216489e48887e2688ac97f',
    }
  },

  methods:{
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
