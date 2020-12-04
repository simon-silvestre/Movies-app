<template>
  <div id="app">
    <header>
      <h2>Movies</h2>
      <form @submit.prevent="fetchMovie">
        <input type="text" v-model="search" placeholder="Search">
      </form>
    </header>
    <div class="movieContainer">
      <div class="movie" v-for="(movie, index) in movies.results" :key="index">
          <img :src="'https://image.tmdb.org/t/p/w1280' + movie.poster_path" alt="">
        <div class="movieinfos">
          <p>{{ movie.title }}</p>
          <div class="note">
            <p>{{ movie.vote_average }}</p>
          </div>
        </div>
        <div class="overview">
            <p>{{ movie.overview }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      search: "",
      apiUrl: 'https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=3fd2be6f0c70a2a598f084ddfb75487c&page=1',
      apiSearch: "https://api.themoviedb.org/3/search/movie?api_key=3fd2be6f0c70a2a598f084ddfb75487c&query='",
      movies: {}
    }
  },
  mounted() {
      fetch(this.apiUrl)
      .then((response) => response.json())
        .then(data => this.movies = data)
  },
  methods: {
     fetchMovie() {
      fetch(this.apiSearch + this.search + "'")
      .then((response) => response.json())
        .then(data => this.movies = data)
        this.search = ""
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    background-color: #131313;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    width: 100%;
    height: 100%;
  }
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    height: 75px;
    background-color: #202020;
  }
  header h2 {
    margin-left: 25px;
    font-weight: bold;
    font-size: 30px;
    color: rgba(255, 255, 255, 0.644);
  }
  header input {
    margin-right: 25px;
    padding: 10px;
    border: 2px solid rgba(255, 255, 255, 0.644);
    border-radius: 30px;
    background-color: transparent;
    color: #fff;
    outline: none;
    padding-left: 15px;
  }
  .movieContainer {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
    height: 100%;
  }
  .movie {
    position: relative;
    width: 300px;
    margin: 1rem;
    border-radius: 5px;
    background-color: #1f1f1f;
    overflow: hidden;
  }
  .movie img {
    width: 100%;
  }
  .movieinfos {
    display: flex;
    justify-content: space-between;
    width: 100%;
    color: rgba(255, 255, 255, 0.877);
    font-size: 18px;
    font-weight: bold;
    padding: 0.5rem 1rem 1rem;
  }
  .movieinfos p {
    width: 200px;
    height: fit-content;
  }
  .movieinfos .note {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 35px;
    background-color: #131313;
    font-size: 16px;
    margin-top: 8px;
  }
  .note p {
    width: fit-content;
  }
  .movie .overview {
    position: absolute;
    width: 100%;
    bottom: 0;
    padding: 2rem;
    background-color: rgba(255, 255, 255, 0.918);
    transition: transform 0.6s ease;
    transform: translateY(100%);
    font-weight: 500;
  }
  .movie:hover .overview {
    transform: translateY(0);
  }
  @media screen and (max-width: 499px) {
     header input{
       width: 120px;
     }
  }
</style>
