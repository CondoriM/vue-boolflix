<template>
    <div class="inline rel" @mouseover="hovM = true" @mouseleave="hovM = false">

        <img class="img-fluid rounded img_holder" :src="cover+film.poster_path" alt="">

        <div v-show="hovM" class="info bg-dark rounded text-start rounded">
            
            <!-- sezione info -->
            <div class="">
                <span>Titolo:{{film.name}}</span><br>
                <span>Titolo Originale:{{film.original_name}}</span>
                <div>
                    {{film.original_language}} 
                    <img :src="'https://flagcdn.com/w20/'+ film.original_language +'.png'" alt="">
                </div>
            </div>

            <!-- sezione stelle -->
            <div class="stars">
                <font-awesome-icon v-for="(star,index) in film.vote_average" :key="index + film.vote_average" icon="fa-solid fa-star" />
                <font-awesome-icon v-for="(starN,index) in 5 - film.vote_average" :key="index - film.vote_average" icon="fa-regular fa-star" /><br>

                <span>Overview:{{film.overview}}</span>
            </div>
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
            hovM: false
        }
    }
}
</script>

<style lang="scss" scoped>

@import '@/assets/scss/variable.scss';

</style>
