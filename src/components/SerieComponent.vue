<template>
    <div class="inline rel">
                
        <img class="img-fluid" :src="cover+serie.poster_path" alt="">

        <div class="info">
            <div class="stars">
                <font-awesome-icon v-for="(star,index) in serie.vote_average" :key="index + serie.vote_average" icon="fa-solid fa-star" />
                <font-awesome-icon v-for="(starN,index) in 5 - serie.vote_average" :key="index - serie.vote_average" icon="fa-regular fa-star" />
            </div>

            <div class="">
                {{serie.name}}
                <div>
                    {{serie.original_language}} 
                    <img :src="'https://flagcdn.com/w20/'+ serie.original_language +'.png'" alt="">
                </div>
                {{serie.vote_average}}
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
        }
    }
}
</script>

<style lang="scss" scoped>

.inline{
    display: inline-block;

}
.rel{
    position: relative;

    .info{
        display: none;
        position: absolute;
        top: 0;
    }
}

</style>