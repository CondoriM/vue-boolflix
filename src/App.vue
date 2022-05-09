<template>
  <div id="app">
    <HeadSite/>
    <form @submit.prevent="search">
      <input type="text" v-model="searchT">
      <button type="submit">Invia</button>
      <div class="container">
        <div class="row">
          <div class="col-2 flex-column" v-for="(film,index) in films" :key="index">
            <div class="col">
              <img class="img-fluid" :src="cover+film.poster_path" alt="">
            </div>

            <div class="col">
              {{film.original_title}}
              {{film.title}}
              {{film.original_language}}
              {{film.vote_average}}
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
      films: '',
      cover: 'https://image.tmdb.org/t/p/original',
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
