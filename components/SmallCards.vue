<template>
  <div class="card-container">
    <div class="card" v-for="movie in movies" :key="movie.id">
      <div class="top">
        <img
          :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="bottom">
        <div class="bottom-top">
          <h1 class="title">{{ movie.title }}</h1>
          <p>1h 5 min</p>
        </div>
        <div class="bottom-bottom">
          <p>
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Adipisci,
            accusantium.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    const res = await fetch(
      'https://api.themoviedb.org/3/movie/popular?api_key=<<api key>>&language=en-US&page=1'
    )
    const data = await res.json()
    this.movies = data.results
    this.movies.splice(3, this.movies.length)
  },
}
</script>

<style lang="scss" scoped>
.card-container {
  display: flex;
  flex-wrap: nowrap;
  gap: 0.5rem;

  .card {
    height: 12rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    width: 20rem;
    background: #000;
    display: grid;
    grid-template-rows: 70% auto;
    .top {
      background: #333;

      img {
        height: 100%;
        width: 100%;
        object-fit: cover;
      }
    }
    .bottom {
      padding: 0 1rem;
      &-top {
        display: flex;
        justify-content: space-between;
        margin-top: -1.5rem;
        color: #fff;
        text-shadow: 0 0 10px rgba(0, 0, 0.5);
        h1 {
          font-weight: 600;
        }
      }
      &-bottom {
        font-size: 0.7rem;
        line-height: 1rem;
        margin-top: 0.5rem;
        color: #fff;
      }
    }
  }
}
</style>
