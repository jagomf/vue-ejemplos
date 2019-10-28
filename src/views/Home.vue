<template>
  <div class="home">
    <div>
      <h3>Crear peli</h3>
      <div>
        <CreateMovie @movie-add="addMovie($event)" />
      </div>
    </div>
    <div class="movies-area">
      <h3>Pelis</h3>
      <input v-model="searchText" placeholder="Filtrar por título" />
      <div v-for="movie in movies" :key="movie.id">
        <MovieItem
          @delete-movie="deleteMovie"
          :movie="movie"
          v-show="containsSearch(movie.title)" />
      </div>
      <div v-if="!hasMovies" class="no-movies">No hay pelis con ese texto</div>
    </div>
    <div class="slots-area">
      <h3>Slots</h3>
      <MainLayout>
        <template v-slot:footer>Cosas enviadas al pie</template>
        <template v-slot:header>Cosas enviadas a la cabecera</template>
        <p>Cosas enviadas desde fuera al centro</p>
      </MainLayout>
    </div>
    <div class="countdown-area">
      <h3>Countdown</h3>
      <CountDown v-model="fromVal" @tick="onTick" @boom="onBoom" />
      <div>Valor visto desde fuera: {{fromVal}}</div>
    </div>
    <HelloWorld nombre="Jago"/>
    <ModelBind />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import ModelBind from '@/components/ModelBind.vue';
import MovieItem from '@/components/MovieItem.vue';
import CountDown from '@/components/CountDown.vue';
import MainLayout from '@/components/MainLayout.vue';
import CreateMovie from '@/components/CreateMovie.vue';

export default {
  name: 'home',
  data() {
    return {
      fromVal: 5,
      searchText: '',
      movies: [
        {
          id: 1,
          pic: 'https://m.media-amazon.com/images/M/MV5BZjdkOTU3MDktN2IxOS00OGEyLWFmMjktY2FiMmZkNWIyODZiXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_UX182_CR0,0,182,268_AL_.jpg',
          title: 'Interstellar',
          description: 'Un hombre va al otro lado del universo para avisar a su hija que se quedó en casa que no le deje ir. Paradójico.',
          type: 'Espacial cuántica',
        },
        {
          id: 2,
          pic: 'https://m.media-amazon.com/images/M/MV5BMTk4ODQzNDY3Ml5BMl5BanBnXkFtZTcwODA0NTM4Nw@@._V1_UX182_CR0,0,182,268_AL_.jpg',
          title: 'The Dark Knight Rises',
          description: 'Batman resurge desde el pozo del mundo para cargarse a la Vane que ha secuestrado Gotham. Se la carga, claro.',
          type: 'Fantástica urbana',
        },
        {
          id: 3,
          pic: 'https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_UX182_CR0,0,182,268_AL_.jpg',
          title: 'Inception',
          description: 'Meterse en los sueños de otras personas es coser y cantar. Además, se acabaron los sueños absurdos. Ya todos son normales.',
          type: 'Filosófica',
        },
        {
          id: 4,
          pic: 'https://m.media-amazon.com/images/M/MV5BMjIxMjgxNTk0MF5BMl5BanBnXkFtZTgwNjIyOTg2MDE@._V1_UX182_CR0,0,182,268_AL_.jpg',
          title: 'Wolf of Wall Street',
          description: 'Leo DiCaprio es un genio del engaño y monta una empresa que funciona y encima es la juerga padre.',
          type: 'Economía del caos',
        },
        {
          id: 5,
          pic: 'https://m.media-amazon.com/images/M/MV5BNDQxOTc0MzMtZmRlOS00OWQ5LWI2ZDctOTAwNmMwOTYxYzlhXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_UX182_CR0,0,182,268_AL_.jpg',
          title: 'Gattaca',
          description: 'Un tipo que pertenecía a una élite de cracks descubre que no lo es cuando las dos piernas le hacen crack. Un desconocido le impersonará para el resto de su vida.',
          type: 'Futuro distópico',
        },
      ],
    };
  },
  computed: {
    hasMovies({ searchText, movies }) {
      if (searchText === '') {
        return true;
      }

      const selectedMovies = movies.filter(movie => this.containsSearch(movie.title));
      return !!selectedMovies.length;
    },
  },
  methods: {
    containsSearch(title) {
      return title.toLowerCase().includes(this.searchText);
    },
    deleteMovie(movieId) {
      const index = this.movies.findIndex(movie => movie.id === parseInt(movieId, 10));
      this.movies.splice(index, 1);
    },
    addMovie(newMovie) {
      this.movies.push(newMovie);
    },
    onTick() {
      // eslint-disable-next-line
      console.log('Tick');
    },
    onBoom() {
      // eslint-disable-next-line
      console.log('Boom');
    },
  },
  components: {
    CreateMovie,
    MainLayout,
    CountDown,
    MovieItem,
    ModelBind,
    HelloWorld,
  },
};
</script>

<style>
.movies-area {
  background-color: silver;
  padding: 10px;
}
.no-movies {
  margin-top: 15px;
  padding: 20px;
  border-radius: 15px;
  border: 3px dashed red;
}

.countdown-area, .slots-area {
  margin: 20px;
  padding: 10px;
  border: 1px solid black;
}
</style>
