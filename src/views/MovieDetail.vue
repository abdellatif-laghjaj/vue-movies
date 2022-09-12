<template>
    <div class="movie-detail">
        <h2 class="title">{{ movie.Title }}</h2>
        <p>Released: {{ movie.Year }}</p>
        <img :src="movie.Poster" :alt="movie.Title">
        <h3>Description:</h3>
        <p>{{ movie.Plot }}</p>
        <h3>Actors:</h3>
        <span class="actor" v-for="(actor, index) in actors" :key="index">
            {{ actor }}
        </span>
    </div>
</template>

<script>
import env from "@/env";
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        const actors = ref([]);
        const api_url = "https://www.omdbapi.com/"
        const id = route.params.id;

        onBeforeMount(() => {
            fetch(`${api_url}?apikey=${env.apikey}&i=${id}&plot=full`)
                .then(res => res.json())
                .then(data => {
                    movie.value = data;
                    actors.value = data.Actors.split(",");
                    console.log(data);
                })
        })

        return {
            movie,
        };
    },
};
</script>

<style lang="scss">
    .movie-detail {
        color: #fff;
        padding: 20px;

        .title {
            font-size: 28px;
            margin-bottom: 20px;
        }
    }
</style>
