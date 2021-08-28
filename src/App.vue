<template>
  <div id="app">
    <!-- Panel central -->
    <img class="img-banner" alt="Pokemon logo" src="./assets/Pokemon.png" />
    <h2 class="my-4">PokeGuía</h2>
    <label class="mr-2">Nombre:</label>
    <input type="text" placeholder="Ingrese un pokémon" v-model="pokemonName" />
    <button @click="searchPokemon()">Buscar</button>
    <!-- Imagen de Pokemon buscado -->
    <div>
      <img :src="pokemonImage" />
    </div>
    <div>
      <h3>Movimientos</h3>
      <p v-for="(pokemonMove, $index) in moves" :key="$index">
        {{ pokemonMove.move.name }}
      </p>
      <h3>Habilidades</h3>
      <p v-for="(pokemonAbility, $index) in abilities" :key="$index">
        {{ pokemonAbility.ability.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    pokemonName: 'pikachu',
    pokemon: null
  }),
  methods: {
    searchPokemon() {
      console.log(this.pokemonName)
      this.fetchPokemon()
    },
    fetchPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`)
        .then((response) => response.json())
        .then((json) => (this.pokemon = json))
    }
  },
  computed: {
    pokemonImage() {
      return (
        this.pokemon &&
        this.pokemon.sprites &&
        this.pokemon.sprites.front_default
      )
    },
    moves() {
      return this.pokemon.moves
    },
    abilities() {
      return this.pokemon.abilities
    }
  },

  created() {
    this.fetchPokemon()
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.img-banner {
  height: 200px;
}
</style>
