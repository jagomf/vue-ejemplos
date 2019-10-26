<template>
  <div class="card">
    <img :src="movie.pic" alt="Movie poster" />
    <div class="movie-content">
      <div class="title">
        <span @click.prevent="onReqDel" class="delete-item">&times;</span>
        <span>{{ movie.title }}</span>
      </div>
      <div class="movie-style">{{ movie.type }}</div>
      <div>{{ movie.description }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieItem',
  props: {
    movie: Object,
  },
  data() {
    return {};
  },
  methods: {
    onReqDel() {
      this.$emit('delete-movie', this.movie.id);
    },
  },
};
</script>

<style>
 .card {
   padding: 10px;
   border: 1px solid black;
   border-radius: 15px;
   margin: 10px;
   background-color: white;
   text-align: left;
   display: flex;
   flex-flow: row nowrap;
 }
 .delete-item {
   color: darkred;
   cursor: pointer;
   font-size: 1.3em;
   float: right;
 }
 .title {
   font-weight: bold;
   font-size: 1.2em;
 }
 .movie-style {
   font-style: oblique;
   color: silver;
 }
 .movie-content {
   display: flex;
   flex-flow: column nowrap;
 }
 img {
   max-height: 100px;
   margin-right: 10px;
 }
</style>
