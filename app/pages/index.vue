<template lang="html">
  <div>
    <header>
      <div>
        <h1>PokeShop</h1>
      </div>
      <div>
        <h2>Marketplace for Pokemon Lover</h2>
      </div>
    </header>
    <section id="search-section">
      <div>
        <h3>Search Pokemon</h3>
      </div>
      <div>
        <v-form>
          <v-text-field
            v-model="searchPokemon"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
          <v-btn color="success" @click="handleSearch">
            Search
          </v-btn>
        </v-form>
      </div>
    </section>
    <section id="display-section">
      <div v-for="pokemon in results" :key="pokemon.id">
        {{ pokemon.name }}
        {{ pokemon.sprites }}
        <!-- <img :src="pokemon.sprites.front_default" :alt="pokemon.name" /> -->
      </div>
    </section>
  </div>
</template>

<script lang="js">
  import axios from 'axios';
  export default {
    data() {
      return {
        searchPokemon: "",
        results: []
      }
    },
    methods: {
      handleSearch() {
        const url = `https://pokeapi.co/api/v2/pokemon/${this.searchPokemon.toLowerCase()}`;
        axios.get(url)
          .then(res => {
            this.results = res.data;
          })
          .catch(err => {
            console.error(err);
            console.log(`[ERROR] Cannot Fetching API.`);
          })
      }
    }
  }
</script>

<style lang="css" scoped>
  * {
    text-align: center;
  }
</style>
