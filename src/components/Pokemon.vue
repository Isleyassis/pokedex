<template>
  <div class="container">
    <h1>Pokédex</h1>
    
    <div class="search">
    <input type="text" class="pesquisa" required>
    <button class="butao-pesquisa"><i class="fas fa-search"></i></button>
    </div>

    <ul class="list-group">
      <li class="list-group-item" v-for="pokemon in api.results" :key="pokemon" v-text="pokemon.name"></li>
    </ul>

    <div class="butoes">
    <button class="btn btn-danger" v-if="api.previous" @click="previous">Previous</button>
    <button class="btn btn-primary" v-if="api.next" @click="next">Next</button>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  
  export default {
    data() {
      return {
        api: {},
      }
    },
    created() {
      this.fetchPokemons();
    },
    methods: {
      fetchPokemons(url = 'http://pokeapi.co/api/v2/pokemon') {
        axios.get(url)
          .then(({ data }) => this.api = data);
      },
      next() {
        this.fetchPokemons(this.api.next);
      },
      previous() {
        this.fetchPokemons(this.api.previous);
      }
    }
  }
</script>

<style scoped>
      h1{
      color: white;
      display: block;
      margin: 5px auto;
      font-weight: bolder;
      font-size: 50px;
      }
     .container h1,
     .butoes{
         display: flex;
         justify-content: center;
         flex-direction: row;
         margin-top: 10px;
     }
     .btn{
         margin: 10px 5px;
     }
     .list-group{
         text-align: center;
         width: 40%;
         display: block;
         margin: 0 auto;
         border-radius: 10px;
         width: 60%;
     }
      .list-group-item:hover{
        color: blue;
        cursor: pointer;
      }
        .pesquisa{
        display: flex;
        border-radius: 10px 0 0 10px;
        height: 30px;
        padding: 3px 10px;
        box-shadow: 2px 2px 10px black;
        border: none;
        outline: none;
        }
        .search{
        display: flex;
        justify-content: center;
        margin: 20px 0;
        }
        .butao-pesquisa{
          height: 30px;
          width: 30px;
          box-shadow: 2px 2px 10px black;
          border-radius: 0 10px 10px 0;
          border: none;
          background-color: white;
        }
</style>