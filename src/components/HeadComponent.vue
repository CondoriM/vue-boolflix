<template>
    <div class="container-fluid">
        <div class="navbar bg-dark">
            <div class="col-2">

            </div>

            <div class="col">
                <input
                    type="text"
                    :value="search"
                    @input="$emit('update:search', $event.target.value)"
                />
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name:'HeadSite',
    props: ['search'],
    emits: ['update:search']
}
</script>
