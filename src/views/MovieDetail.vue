<template>
    <div class="movie-detail">
        <h2 class="title">{{ movie.Title }}</h2>
        <p class="date">Released: {{ movie.Year }}</p>
        <img :src="movie.Poster" :alt="movie.Title">
        <div class="rating">
            <box-icon type='solid' name='star' color="#FFB200"></box-icon> {{ movie.imdbRating }}
        </div>
        <h3>Description:</h3>
        <p class="plot">{{ movie.Plot }}</p>
        <h3>Genre:</h3>
        <span class="genre" v-for="(genre, index) in genres" :key="index">
            {{ genre }}
        </span>
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
import 'boxicons'
export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        const actors = ref([]);
        const genres = ref([]);
        const api_url = "https://www.omdbapi.com/"
        const id = route.params.id;

        onBeforeMount(() => {
            fetch(`${api_url}?apikey=${env.apikey}&i=${id}&plot=full`)
                .then(res => res.json())
                .then(data => {
                    movie.value = data;
                    actors.value = data.Actors.split(", ");
                    genres.value = data.Genre.split(", ");
                })
        })

        return {
            movie,
            actors,
            genres,
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

        img{
            width: 200px;
        }

        .rating {
            display: flex;
            justify-content: start;
            align-items: center;
            gap: 8px;
            margin: 8px 0;
        }

        .date{
            margin-bottom: 8px;
        }

        h3{
            font-size: 20px;
            margin: 12px 0;
        }

        .genre, .actor{
            background-color: #42B883;
            padding: 8px 4px;
            border-radius: 4px;
            margin-right: 8px;
        }
    }
</style>
