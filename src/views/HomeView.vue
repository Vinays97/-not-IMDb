<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt3501632">
        <img src="https://m.media-amazon.com/images/M/MV5BMjMyNDkzMzI1OF5BMl5BanBnXkFtZTgwODcxODg5MjI@._V1_SX300.jpg"
          alt="Thor Poster" class="feature-img" />
        <div class="featured">FEATURED</div>
        <div class="detail">
          <h3>Thor: Ragnarok</h3>
          <p>Imprisoned on the other side of the universe,
            the mighty Thor (Chris Hemsworth) finds himself in a
            deadly gladiatorial contest that puts him against
            The Incredible Hulk (Mark Ruffalo),
            his former ally and fellow Avenger.</p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Type to search..." aria-label="Search" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';
import env from '@/env';

export default {
  setup() {
    const search = ref('');
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value !== '') {
        axios.get(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => {
            movies.value = response.data.Search;
            search.value = '';
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .feature-img {
      display: block;
      width: 100%;
      height: auto;
      max-height: 500px;
      object-fit: cover;

      position: relative;
      z-index: 0;
    }

    .featured {
      position: absolute;
      padding: 8px 16px;
      background-color: #f5c517;
      color: #000000;
      top: 16px;
      left: 0px;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color: #ffffff;
        margin-bottom: 16px;
      }

      p {
        color: #ffffff;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #ffffff;
        background-color: #3c434c;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &:focus {
          outline: none;
          border: 1px solid #f3f3f3;
        }

        &::placeholder {
          color: #f3f3f3;
        }
      }

      &[type='submit'] {
        width: 100%;
        max-width: 300px;
        background-color: #f5c517;
        padding: 16px;
        border-radius: 8px;
        color: #000000;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #282b35;
        }
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

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
            height: 250px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #f5c517;
            color: #000000;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #282b35;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #aaaaaa;
            font-size: 14px;
          }

          h3 {
            color: #ffffff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>
