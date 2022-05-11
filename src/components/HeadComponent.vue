<template>
    <div class="container-fluid">
        <div class="row">
            <div class="navbar bg-dark justify-content-between">
                <div class="col-2">
                    <img class="img-fluid" src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
                </div>

                <div class="col text-end">
                    <form @submit.prevent="$emit('formSubmit')">
                        <input type="text" :value="searchT"
                        v-on:input="$emit('input', $event.target.value)"
                        />
                    </form>
                </div>
            </div>
        </div>
    </div>  
</template>

<script>
export default{
    name:'HeadSite',
    props: {
        searchT: String
    },
}
</script>
