<template>
  <div class="card-container">
    <NuxtLink :to="`/movies/${movie.id}`">
      <div
        class="card"
        :style="{
          background:
            'url(' + `https://image.tmdb.org/t/p/w500${movie.poster_path}` ||
            '~/assets/bg.png' + ')',
        }"
      >
        <h1 class="top-rating">{{ movie.vote_average }}</h1>
        <div class="details">
          <h1 class="title">{{ movie.title }}</h1>
          <div class="duration">{{ movie.release_date }}</div>
        </div>
        <div class="hide-container">{{ movie.overview }}</div>
      </div>
    </NuxtLink>
  </div>
</template>

<script>
export default {
  props: ['movie'],
}
</script>

<style lang="scss" scoped>
.card-container {
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
      gap: 0.5rem;
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
