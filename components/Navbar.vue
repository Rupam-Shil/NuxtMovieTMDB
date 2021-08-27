<template>
  <div class="navbar">
    <h1 class="navbar__header">filmography.</h1>
    <ul>
      <li class="active">Home</li>
      <li>Movies</li>
      <li>TV Series</li>
      <li>Top Rated</li>
    </ul>
    <div class="navbar__signup">
      <p>Register/Login</p>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.navbar {
  position: absolute;
  width: 85%;
  height: 3rem;
  background: rgb(37, 37, 37);
  color: #fff;
  display: grid;
  align-items: center;
  grid-template-columns: 20% 60% auto;
  box-shadow: 0 10px 25px rgba(53, 53, 53, 0.5);
  top: 2rem;
  right: 2rem;
  &__header {
    margin-left: 2rem;
    font-weight: 700;
  }
  ul {
    display: flex;
    gap: 2rem;
    height: 100%;
    li {
      display: grid;
      place-content: center;
      height: 100%;
      &.active {
        border-bottom: 3px solid #fff;
      }
    }
  }
  &__signup {
    background-color: #0093e9;
    background-image: linear-gradient(160deg, #0093e9 0%, #80d0c7 100%);
    font-weight: 600;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
@media only screen and (max-width: 900px) {
  ul {
    li {
      display: none !important;
    }
  }
  .navbar__signup {
    display: none;
  }
}
</style>
