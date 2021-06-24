<template>
  <div id="app">
    <Header />

    <main>
      <CustomForm 
      inputPlaceholder="SCRIVI QUI IL NOME"
      @sendForm="searchPokemon"
      />

      <CustomForm 
      inputPlaceholder="SCRIVI QUI LA TIPOLOGIA"
      @sendForm="searchType"
      />

      <Cards 
      :items="pokemons"
      />
    </main>
    
  </div>
</template>

<script>

import axios from "axios";

import Header from './components/Header';
import Cards from './components/Cards';
import CustomForm from './components/CustomForm';

export default {
  name: 'App',
  components: {
    Header,
    Cards,
    CustomForm
  },
  data: function() {
    return {
      base_url: 'https://pokeapi.co/api/v2/',
      pokemons: []
    }
  },
  methods: {
    searchPokemon: function(text) {
      // console.log(text);
      axios
        .get(`${this.base_url}pokemon/${text}`)
        .then(
          (res) => {
            // console.log(res.data);
            this.pokemons = [
              {
                name: res.data.name,
                url: `${this.base_url}pokemon/${text}`,
                img: res.data.sprites.other.dream_world.front_default
              }
            ];
          }
        )
        .catch(
          (err) => {
            console.log(err);
            this.pokemons = [];
          }
        )
    },
    searchType: function(text) {
      // console.log(text);
      axios
        .get(`${this.base_url}type/${text}`)
        .then(
          (res) => {
            // console.log(res.data.pokemon);

            this.pokemons = res.data.pokemon.map(
              (element) => {

              const urlArray = element.pokemon.url.split("/");
              const pokemonId = urlArray[urlArray.length - 2];
              const imgPath = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemonId}.svg`;
              
              return {
                ...element.pokemon,
                img: imgPath
              };
            }
            );
          }
        )
        .catch(
          (err) => {
            console.log(err);
          }
        )
    }
  },
  created: function() {
    axios
      .get(`${this.base_url}pokemon`)
      .then(
        (res) => {
          // console.log(res.data);
          // this.pokemons = res.data.results

          // Versione forEach 

          // this.pokemons.forEach(
          // (element) => {
          //   const urlArray = element.url.split("/");
          //   const pokemonId = urlArray[urlArray.length - 2];
          //   // console.log(urlArray);
          //   console.log(pokemonId);
          // });

          // versione map

          this.pokemons = res.data.results.map(
            (element) => {
              const urlArray = element.url.split("/");
              const pokemonId = urlArray[urlArray.length - 2];
              const imgPath = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemonId}.svg`;
              
              return {
                ...element,
                img: imgPath
              };
            }
          );
        }
      )
      .catch(
        (err) => {
          console.log(err);
        }
      )
  }
}
</script>

<style lang="scss">

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

main {
  width: 80%;
  margin: 30px auto;
}

</style>
