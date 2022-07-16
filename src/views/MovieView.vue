<template>
  <div class="movie-detail">
    <img :src="movie.Poster" alt="Movie Poster" class="feature-img" />
    <strong>{{ movie.Title }}</strong>
    <div class="details">
      <p>{{ movie.Year }} • {{ movie.Genre }} • {{ movie.Runtime }}</p>
    </div>
    <div class="rating">
      <p>(not)IMDb Rating: {{ movie.imdbRating }}</p>
    </div>
    <div class="extra-details">
      <h1>Plot</h1>
      <p>{{ movie.Plot }}</p>
      <h1>Actors</h1>
      <p>{{ movie.Actors }}</p>
      <h1>Country of Origin</h1>
      <p>{{ movie.Country }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import axios from 'axios';
import env from '@/env';

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      axios.get(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then((response) => {
          movie.value = response.data;
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style lang="scss">
.movie-detail {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 16px;

  .feature-img {
    display: block;
    width: 50%;
    max-width: 300px;
    border-radius: 12px;
    margin-bottom: 8px;
    margin-bottom: 16px;
  }

  strong {
    color: #ffffff;
    font-size: 28px;
    font-weight: 600;
  }

  .details {
    width: 100%;
    text-align: center;
    margin-top: 4px;

    p {
      color: rgba($color: #FFFFFF, $alpha: 0.6);
      font-size: 16px;
      font-weight: 400;
    }
  }

  .rating {
    width: 100%;
    text-align: center;
    margin-top: 4px;

    p {
      color: rgba($color: #f5c517, $alpha: 0.9);
      font-size: 16px;
      font-weight: 400;
    }
  }

  .extra-details {
    width: 100%;
    text-align: left;

    h1 {
      margin-top: 12px;
      color: rgba($color: #FFFFFF, $alpha: 0.6);
      font-size: 18px;
      margin-bottom: 8px;
      font-weight: 400;
    }

    p {
      justify-content: left;
      color: #ffffff;
      font-size: 18px;
    }
  }
}
</style>
