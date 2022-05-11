<template>
    <div class="inline rel" @mouseover="hovM = true" @mouseleave="hovM = false">
                
        <img class="img-fluid rounded" :src="cover+serie.poster_path" alt="">

        <div v-show="hovM" class="info bg-dark rounded text-start rounded">

            <!-- sezione info -->
            <div class="">
                <span>Titolo:{{serie.name}}</span><br>
                <span>Titolo Originale:{{serie.original_name}}</span>
                <div>
                    {{serie.original_language}} 
                    <img :src="'https://flagcdn.com/w20/'+ serie.original_language +'.png'" alt="">
                </div>
            </div>

            <!-- sezione stelle -->
            <div class="stars">
                <font-awesome-icon v-for="(star,index) in serie.vote_average" :key="index + serie.vote_average" icon="fa-solid fa-star" />
                <font-awesome-icon v-for="(starN,index) in 5 - serie.vote_average" :key="index - serie.vote_average" icon="fa-regular fa-star" /><br>

                <!-- overview programma -->
                <span>Overview:{{serie.overview}}</span>
            </div>
        </div>     
    </div>
</template>

<script>
export default {
    name: 'SerieComp',
    props:{
        serie: Object,
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

.inline{
    display: inline-block;
    max-width: 342px;
}
.rel{
    position: relative;

    .info{
        position: absolute;
        top: 0;
        padding: 1rem;
        width: 100%;
        height: 100%;
        overflow-y: scroll;
    }
}

</style>