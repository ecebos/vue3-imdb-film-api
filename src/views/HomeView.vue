<template>
 <div>
  <h4>IMDB FİLM LİSTESİ</h4>
    <input v-model="searchQuery" @keyup="filterMovie()" type="text" placeholder="Film ara...">
    <div class="movie-list">
      <div v-if="!movies.length">Listelenecek içerik bulunamadı</div>
      <div v-for="movie in movies" :key="movie.imdbID" class="movie-item">
        <div class="movie">
          <img :src="movie.Poster" :alt="movie.Title">
          <h5>{{ movie.Title }}</h5>
          <span>{{ movie.Year }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap";

export default {
  name: 'MovieList',
  data() {
    return {
      movies: [],
      searchQuery: ''
    }
  },
  mounted() {
     
  },
  computed: {
    // filteredMovies() {
    //   return this.movies.filter(movie => {
    //     return movie.Title.toLowerCase().includes(this.searchQuery.toLowerCase());
    //   });
    // }
  },
  methods:{
    filterMovie(){
      if(this.searchQuery.length>2){
        axios.get('https://www.omdbapi.com/?apikey=ada32395&s='+ this.searchQuery)
      .then(response => {
        this.movies = response.data.Search;
      })
      }
      
    }
  }
}
</script>
<style>

.movie-list {
  display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 40px;
    align-items: center;
}

.movie-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 10px 20px;
}

.movie {
  text-align: center;
    border: 1px solid black;
    padding: 10px;
    display: flex;
    align-items: stretch;
    flex-direction: column;
    flex-wrap: wrap;
}
input{
  border-radius: 10px;
    border: 2px solid gray;
    margin-top: 10px;
    width: 25%;
    height: 33px;
    font-size: 13px;
    padding: 2px 2px 2px 6px;
}
img{
  object-fit: contain;
}
h4{
  margin-top: 20px;
    font-weight: bold;
    color: #4f4d4d;
}
</style>
