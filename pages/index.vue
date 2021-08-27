<template>
  <div>
    <Navbar />
    <section class="first">
      <div class="hero">
        <div class="hero__left">
          <p>
            Lorem ipsum dolor sit amet consectetur . Voluptas similique vitae
            optio.
          </p>
        </div>
        <div class="hero__right">
          <div class="search">
            <h1>Find <span>perfect</span> movie for evening</h1>
            <div class="search-area">
              <input
                type="text"
                placeholder="Search Here"
                v-model="serachValue"
              />
              <button type="button" @click.prevent="getRequiredMovie">
                GIVE ME THIS!
              </button>
            </div>
          </div>
          <div class="bottom">
            <div class="bottom__left">
              <h1>Top of the last week</h1>
              <p>The collection of top movies from last week</p>
            </div>
            <div class="bottom__right">
              <SmallCards />
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="second">
      <div class="left"></div>
      <div class="right">
        <h1 class="header">Straight form horse's mouth</h1>
        <div class="bigcardcontainer" v-if="serachValue === ''">
          <BigCards v-for="movie in topMovies" :key="movie.id" :movie="movie" />
        </div>
        <div class="bigcardcontainer" v-else>
          <BigCards
            v-for="movie in requireMovie"
            :key="movie.id"
            :movie="movie"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      serachValue: '',
      topMovies: [],
      requireMovie: [],
    }
  },
  async fetch() {
    const res = await fetch(
      'https://api.themoviedb.org/3/movie/top_rated?api_key=<<api key>>&language=en-US&page=1'
    )
    const data = await res.json()
    this.topMovies = data.results
  },
  methods: {
    async getRequiredMovie() {
      this.serachValue = this.serachValue.trim().replace(' ', '-')
      const res = await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=<<api key>>&language=en-US&query=${this.serachValue}&page=all&include_adult=false`
      )
      const data = await res.json()
      this.requireMovie = data.results
      window.scrollTo({
        top: 900,
        behavior: 'smooth',
      })
    },
  },
}
</script>

<style lang="scss" scoped>
section.first {
  width: 100vw;
  height: 90vh;
  .hero {
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 5% auto;

    &__left {
      display: flex;
      justify-content: center;
      align-items: center;
      p {
        writing-mode: vertical-rl;
      }
    }
    &__right {
      background: #333 url('~/static/bg.png');
      background-repeat: no-repeat;
      background-size: cover;
      display: grid;
      grid-template-rows: 80% 20%;
      .search {
        margin-top: 2rem;

        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        text-align: center;
        h1 {
          font-size: clamp(2rem, 10vw, 3rem);
          font-weight: 500;
          color: #fff;
          text-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
          margin-bottom: 2rem;
          span {
            font-weight: 800;
          }
        }
        &-area {
          display: flex;
          align-items: center;
          justify-content: center;
          width: 80%;
          input {
            width: 50%;
            min-width: 200px;
            height: 50px;
            padding: 1rem;
            border-radius: 0.5rem 0 0 0.5rem;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.5);
          }
          button {
            height: 50px;
            display: inline-block;
            border-radius: 0 0.5rem 0.5rem 0;
            box-shadow: 5px 0 10px rgba(0, 0, 0, 0.3);
            background: rgb(0, 225, 255);
            padding: 0 1rem;
            color: #fff;
            font-weight: 600;
          }
        }
      }
      .bottom {
        display: grid;
        grid-template-columns: 30% auto;
        padding: 2rem;
        &__left {
          color: #fff;
          h1 {
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            font-size: 1.5rem;
            font-weight: 500;
          }
          p {
            color: rgb(7, 7, 7);
          }
        }
        &__right {
          // display: flex;
          // flex-wrap: nowrap;
          // gap: 0.5rem;
        }
      }
    }
  }
}

section.second {
  margin-top: 9rem;
  width: 100vw;
  height: 20px;
  display: grid;
  grid-template-columns: 5% auto;
  .right {
    .header {
      font-size: 2rem;
      font-weight: 700;
      margin-bottom: 2rem;
    }
    .bigcardcontainer {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-bottom: 2rem;
      padding-right: 2rem;
    }
  }
}
@media only screen and (max-width: 900px) {
  .hero {
    grid-template-columns: 100% !important;
    &__left {
      display: none !important;
    }
    button {
      font-size: 12px;
      padding: 0 0.2rem !important;
    }
  }
  .bottom {
    display: none !important;
  }
}
</style>
