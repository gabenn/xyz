<template>
    <div class="container">
        {{ id }}
        <h3>Other {{ type }} Pokemons:</h3>
        <p v-for="(similar, index) in similarPokemons">
            <SimilarCard
                :similar="similar"
                :id="index"
                @click="selectSimilarPokemon(similar)"
            />
        </p>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import SimilarCard from "@/components/SimilarCard.vue";

export default defineComponent({
    name: "SimilarContainer",
    components: { SimilarCard },
    props: ["similarPokemons", "type", "id"],
    emits: ["changePokemon"],
    methods: {
        selectSimilarPokemon(similar: any) {
            const pokemonId = similar.pokemon.name;

            this.$emit("changePokemon", pokemonId);
        },
    },
    mounted() {
        // console.log(this.similarPokemons);
    },
});
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
}
</style>
