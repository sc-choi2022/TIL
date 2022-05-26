<template>
  <div>
    <div><h1>Home</h1></div><hr>
    <div class="container">
      <div class="box"><img :src="cardUrl + movies[0].poster_path" alt="movie_poster" class="poster-1"></div>
      <div class="box"><img :src="cardUrl + movies[1].poster_path" alt="movie_poster" class="poster-1"></div>
      <div class="box"><img :src="cardUrl + movies[2].poster_path" alt="movie_poster" class="poster-2"></div>
      <div class="box"><img :src="cardUrl + movies[3].poster_path" alt="movie_poster" class="poster-3"></div>
      <div class="box"><img :src="cardUrl + movies[4].poster_path" alt="movie_poster" class="poster-4"></div>     
    </div>
  </div>
</template>

<script>
  import { mapActions, mapGetters } from 'vuex'

  export default {
    name: 'MovieList',
    computed: {
      ...mapGetters(['movies']),
      cardUrl(){
        return "https://image.tmdb.org/t/p/w400"
      }
    },
    methods: {
      ...mapActions(['fetchMovies'])
    },
    created() {
      this.fetchMovies()
    },
  }
</script>

<style>
.posters {
  display: flex;
  width: 100%;
  box-sizing: border-box;
  height: 100vh;
}
.box {
  flex: 1;
  overflow: hidden;
  transition: .5s;
  margin: 0 2%;
  box-shadow: 0 10px 10px rgba(0,0,0,.1);
  line-height: 0;
}

box > img {
  width: 200%;
  height: calc(100% - 10vh);
  object-fit: cover; 
  transition: .5s;
}

.box:hover { flex: 1 1 50%; }
.box:hover > img {
  width: 60%;
  height: 60%;
}
</style>

