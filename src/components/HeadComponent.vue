<template>
    <div class="container-fluid">
        <div class="navbar bg-dark">
            <div class="col-2">

            </div>

            <div class="col">
                <form @submit.prevent="$emit('formSubmit')">
                    <input type="text" :value="searchT"
                    v-on:input="$emit('input', $event.target.value)"
                    />

                    <button type="submit">Invia</button>
                </form>
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
