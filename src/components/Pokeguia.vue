<template>
  <div>
    <h1 class="titulo">PokeGuía</h1>
    <v-row class="row">
      <v-col class="columna">
        <label class="nombre">Busca tu pokemon por nombre:</label>
      </v-col>
      <v-col>
        <v-text-field
          v-model="pokemon.name"
          v-on:keyup.enter="pokeApi"
          hide-details
          solo
          required
        />
      </v-col>
      <v-col>
        <v-btn @click="pokeApi" rounded dark>Buscar</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <img :src="picture" class="imagen" />
        <h2 class="pokename">{{ pokeName }}</h2>
      </v-col>
      <v-col>
        <h2>Movimientos</h2>
        <v-virtual-scroll
          class="card"
          :items="movements"
          :item-height="30"
          height="230"
        >
          <template v-slot:default="{ item }">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>{{ item.move.name }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-virtual-scroll>
      </v-col>
      <v-col>
        <h2>Habilidades</h2>
        <v-virtual-scroll
          class="card"
          :items="abilities"
          :item-height="30"
          height="230"
        >
          <template v-slot:default="{ item }">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>{{ item.ability.name }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-virtual-scroll>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "Pokeguia",
  data() {
    return {
      pokemon: {
        name: "plusle",
        sprites: {
          other: {
            dream_world: {
              front_default: "",
            },
          },
        },
        moves: [],
        abilities: [],
      },
    };
  },
  created() {
    this.pokeApi();
  },
  methods: {
    pokeApi() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`)
        .then((response) => response.json())
        .then((json) => (this.pokemon = json));
    },
  },
  computed: {
    picture() {
      return this.pokemon.sprites.other.dream_world.front_default;
    },
    movements() {
      return this.pokemon.moves;
    },
    abilities() {
      return this.pokemon.abilities;
    },
    pokeName() {
      return this.pokemon.name;
    },
  },
};
</script>

<style>
.titulo {
  font-size: 40px;
  margin-bottom: 20px;
}
.imagen {
  height: 250px;
}
.card {
  backdrop-filter: blur(11px) saturate(197%);
  -webkit-backdrop-filter: blur(11px) saturate(197%);
  background-color: rgba(255, 255, 255, 0.17);
  border-radius: 12px;
  border: 1px solid rgba(209, 213, 219, 0.3);
  margin-top: 10px;
}
.columna {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  font-size: 25px;
  font-weight: bold;
}
.pokename {
  font-size: 30px;
  margin-top: 9px;
  font-weight: bold;
}
h2 {
  font-size: 30px;
}
</style>
