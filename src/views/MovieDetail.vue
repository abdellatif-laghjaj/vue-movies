<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
  </div>
</template>

<script>
import env from "@/env";
import { ref, onBeforeMount } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();
    const api_url = "https://www.omdbapi.com/"

    onBeforeMount(() => {
        console.log(route.params.id);
    })

    return {
      movie,
    };
  },
};
</script>

<style lang="scss"></style>
