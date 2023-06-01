<template>
    <div class="container">
        <div class="search_form">
            <input
                type="text"
                id="name"
                placeholder="Your favourite pokemon"
                v-model="id"
            />
            <input type="button" value="Search" @click="getPokemon(id)" />
        </div>
        <PokemonCard v-if="pokemon.exists" :pokemon="pokemon" />
        <SimilarContainer
            v-if="pokemon.exists"
            :similarPokemons="similarPokemons"
            :type="pokemon.firstType"
            :id="id"
            @changePokemon="(id) => emitedSearch(id)"
        />
    </div>
</template>

<script lang="ts">
import PokemonCard from "@/components/PokemonCard.vue";
import SimilarContainer from "@/components/SimilarContainer.vue";
import { defineComponent } from "vue";

export default defineComponent({
    name: "SearchView",
    data() {
        return {
            id: "",
            pokemon: {
                name: String,
                src: String,
                types: [],
                weight: Number,
                height: Number,
                firstType: "",
                exists: false,
            },
            similarPokemons: [],
        };
    },
    components: {
        PokemonCard,
        SimilarContainer,
    },
    methods: {
        clearPoke() {
            this.pokemon = {
                name: String,
                src: String,
                types: [],
                weight: Number,
                height: Number,
                firstType: "",
                exists: false,
            };
            this.similarPokemons = [];
        },
        getPokemon(id: String) {
            const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
            fetch(url)
                .then((res) => res.json())
                .then((res) => {
                    this.pokemon.name = res.name;
                    this.pokemon.src = res.sprites.front_default;

                    this.pokemon.types = res.types.map((type: any) => {
                        this.pokemon.firstType +=
                            this.pokemon.firstType === "" ? type.type.name : ""; //tuti można jakoś lepiej
                        return type.type.name;
                    });
                    this.pokemon.weight = res.weight;
                    this.pokemon.height = res.height;
                    this.pokemon.exists = true;
                    this.id = "";
                    this.getPokemonsFromType(this.pokemon.firstType);
                })
                .catch((err) => {
                    console.log(err);
                    return err;
                });
        },
        getPokemonsFromType(type: String): any {
            const url = `https://pokeapi.co/api/v2/type/${type}`;
            fetch(url)
                .then((res) => res.json())
                .then((res) => {
                    res = res.pokemon;
                    const ran =
                        res.length > 20
                            ? Math.floor((Math.random() * res.length) / 10)
                            : 0;
                    const min = ran * 10;
                    console.log(
                        ran,
                        res.length / 10,
                        res.slice(0 + ran * 10, 10 + ran * 10)
                    );
                    this.similarPokemons = res.slice(min, min + 10);
                });
        },
        emitedSearch(id: String) {
            this.clearPoke();
            this.getPokemon(id);
        },
    },
    mounted() {},
});
</script>
<style scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.search_form {
    padding: 0 0 40px 0;
}
</style>
