<template>
  <div class="card-container">
    <div
      class="card"
      v-for="movie in movies"
      :key="movie.id"
      :style="{
        background:
          'url(' + `https://image.tmdb.org/t/p/w500${movie.poster_path}` + ')',
      }"
    >
      <h1 class="top-rating">{{ movie.vote_average }}</h1>
      <div class="details">
        <h1 class="title">{{ movie.title }}</h1>
        <div class="duration">1h 7min</div>
      </div>
      <div class="hide-container">{{ movie.overview }}</div>
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
      'https://api.themoviedb.org/3/movie/top_rated?api_key=583d845d2de5224f7a09b96f8fc76502&language=en-US&page=1'
    )
    const data = await res.json()
    this.movies = data.results
  },
}
</script>

<style lang="scss" scoped>
.card-container {
  width: 98%;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
  .card {
    border-radius: 1rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    position: relative;
    height: 30rem;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    background-color: #333 !important;
    background-position: center center;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover !important;
    background-blend-mode: soft-light !important;

    .top-rating {
      position: absolute;
      top: 1rem;
      left: 1rem;
      font-weight: 700;
      color: #fff;
    }
    .details {
      display: flex;
      justify-content: space-between;
      margin-bottom: 1rem;
      padding: 0 1rem;
      color: #fff;
      text-shadow: 0 0 10px rgba(0, 0, 0, 0.9);
    }
    .title {
      font-weight: 700;
    }
    .duration {
      font-weight: 300;
    }
    .hide-container {
      width: 100%;
      height: 20rem;
      background: rgb(63, 181, 251);
      background: radial-gradient(
        circle,
        rgba(63, 181, 251, 1) 0%,
        rgba(70, 252, 216, 1) 100%
      );
      margin-bottom: -20rem;
      transition: 0.3s;
      padding: 1rem;
    }
    &:hover .hide-container {
      margin-bottom: 0rem;
    }
  }
}
</style>
