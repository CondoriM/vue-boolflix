<template>
    <div class="container-fluid">
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
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'MainSite',
    data:{
        
    }
}
</script>
