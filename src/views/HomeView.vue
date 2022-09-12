<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0388629">
        <img class="featured-image"
          src="https://w0.peakpx.com/wallpaper/525/657/HD-wallpaper-one-piece-brook-one-piece-chopper-predator-franky-one-piece-jinbe-one-piece-monkey-d-luffy-nami-one-piece-nico-robin-roronoa-zoro-sanji-one-piece-usopp-one-piece.jpg"
          alt="One piece" />
        <div class="detail">
          <h3>One Piece</h3>
          <p>
            Follows the adventures of Monkey D. Luffy and his pirate crew in
            order to find the greatest treasure ever left by the legendary
            Pirate, Gold Roger. The famous mystery treasure named One Piece.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies" class="search-box">
      <input type="text" placeholder="Search for your favorite movie..." v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" :alt="movie.Title">
            <div class="type">{{ movie.Type }}</div>
            <div class="detail">
              <p class="year">{{ movie.Year }}</p>
              <h3>{{ movie.Title }}</h3>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import env from '@/env.js';
import { ref } from 'vue'
export default {
  setup() {
    const search = ref('')
    const movies = ref([])
    const api_url = ref("https://www.omdbapi.com/")
    
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`${api_url}?apikey=${env.apikey}&s=${search.value}`)
          .then(res => res.json())
          .then(data => {
            movies.value = data.Search
            search.value = ""
            console.log(data.Search)
          })
      } else {
        alert("Please enter a movie title")
      }
    }

    return {
      search,
      movies,
      SearchMovies,
    }
  },
};

</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-image {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      padding: 16px;
      z-index: 1;
      background-color: rgba(0, 0, 0, 0.6);
      color: #fff;

      h3 {
        margin-bottom: 16px;
      }
    }
  }

  .search-box {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        padding: 10px 16px;
        border-radius: 6px;
        font-size: 16px;
        color: #fff;
        background-color: #334455;
        margin-bottom: 16px;
        transition: all 0.4s ease-in-out;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        background-color: #42B883;
        border-radius: 8px;
        padding: 12px 16px;
        color: #fff;
        font-size: 18px;
        text-transform: uppercase;
        transition: all 0.3s ease-in-out;
        cursor: pointer;

        &:active {
          transform: scale(0.95);
        }
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
            transition: all 0.4s ease-in-out;

            &:hover {
              opacity: 0.5;
            }
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #fff;
            border-radius: 0 8px 8px 0;
            top: 16px;
            left: 0;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #334455;
          padding: 16px 8px;
          flex: 1 1 100%;
          color: #fff;
          border-radius: 0 0 8px 8px;

          .year {
            font-size: 14px;
            margin-bottom: 8px;
          }

          h3 {
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>
