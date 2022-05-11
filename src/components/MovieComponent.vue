<template>
    <div class="row">
        <div class="col">
            <img class="img-fluid" :src="cover+film.poster_path" alt="">
        </div>

        <div class="stars">
            <font-awesome-icon v-for="(star,index) in film.vote_average" :key="index + film.vote_average" icon="fa-solid fa-star" />
            <font-awesome-icon v-for="(starN,index) in 5 - film.vote_average" :key="index - film.vote_average" icon="fa-regular fa-star" />
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
</template>

<script>
export default {
    name: 'MovieComp',
    props:{
        film: Object,
    },

    data(){
        return{
            cover: 'https://image.tmdb.org/t/p/w342',
        }
    }
}
</script>
