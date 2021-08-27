<template>
  <div class="movie__section">
    <div class="top">
      <NuxtLink to="/"> <button class="back-btn">← Go Back</button> </NuxtLink>
    </div>
    <div class="bottom">
      <div class="poster">
        <img
          :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="details">
        <div class="details-each">
          <h1>Title</h1>
          :
          <p>{{ movie.title }}</p>
        </div>
        <div class="details-each">
          <h1>Ratings</h1>
          :
          <p>{{ movie.vote_average }}</p>
        </div>
        <div class="details-each">
          <h1>Duration</h1>
          :
          <p>{{ movie.runtime }}m.</p>
        </div>
        <div class="details-each">
          <h1>Revenue</h1>
          :
          <p>{{ movie.revenue }}</p>
        </div>
        <div class="details-each">
          <h1>Release</h1>
          :
          <p>{{ movie.release_date }}</p>
        </div>
        <div class="details-each">
          <h1>Budget</h1>
          :
          <p>${{ movie.budget }}</p>
        </div>
        <div class="details-each">
          <h1>Overview</h1>
          :
          <p>{{ movie.overview }}</p>
        </div>
      </div>
    </div>
    <div class="container"></div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    const movie = await $axios.$get(
      `https://api.themoviedb.org/3/movie/${params.id}?api_key=<<api key>>&language=en-US`
    )
    return { movie }
  },
}
</script>

<style lang="scss" scoped>
.movie__section {
  height: 100vh;
  width: 100vw;
  border: 0.5rem solid rgb(0, 217, 255);
  padding: 2rem;
  display: grid;
  gap: 1rem;
  grid-template-rows: 5% 95%;
  .back-btn {
    display: block;
    padding: 0.5rem 1rem;
    background-color: #0093e9;
    background-image: linear-gradient(160deg, #0093e9 0%, #80d0c7 100%);
    color: #fff;
  }
  .bottom {
    display: grid;
    grid-template-columns: 400px auto;
    gap: 2rem;
    .poster {
      background: red;
      img {
        height: 100%;
        width: 100%;
      }
    }
    .details {
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 1rem;
      &-each {
        display: grid;
        grid-template-columns: 20% 5% auto;
        h1 {
          font-size: 1.5rem;
        }
        p {
          font-size: 1.2rem;
        }
      }
    }
  }
}
@media only screen and (max-width: 900px) {
  .movie__section {
    width: unset;
    height: max-content;
  }
  .bottom {
    display: grid;
    grid-template-columns: 100% !important;
    grid-template-rows: auto 800px;
    .details {
    }
  }
}
</style>
