<template>
    <ul>
        <li v-for="pl in players" v-bind:key="pl.id">{{ pl.name }} {{ pl.score }}</li>
    </ul>
    <button class="btn" v-for="pl in players" v-bind:key="pl.id">{{ pl.id}} {{ pl.name }}</button>
</template>

<script>

export default {
    name: 'playerStats',
    props: ['players'],
    methods: {

    }
}
</script>

<style>

ul {
    border: 3px solid #666;
    max-width: 100px;
    background-color: rgb(0, 0, 0) ;
    opacity: 50%;
    display:block;
    margin: 0 auto;
}
li {
    border: 2px solid #666;
}
.btn{
    display: inline;
    margin-left: 50px;
}
</style>
