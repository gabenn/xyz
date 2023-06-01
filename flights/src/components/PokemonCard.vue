<template>
    <div class="card">
        <div class="card_image">
            <img :src="pokemon.src" />
        </div>
        <div class="card_content">
            <h2>{{ pokemon.name }}</h2>
            <div class="types">
                {{ pokemon.types.length > 1 ? "Types:" : "Type:" }}
                <span v-for="type in pokemon.types"> {{ type }}</span>
            </div>
            <div class="details">
                <span class="detail">Height: {{ pokemon.height }}</span>
                <span class="detail">Weight: {{ pokemon.weight }}</span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "PokemonCard",
    props: { pokemon: { type: Object, required: true } },
});
</script>

<style scoped>
.card {
    width: 300px;
    height: 450px;
    border: 1px solid black;
    border-radius: 20px;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.card_image {
    width: 100%;
    height: 50%;
    padding-bottom: 20px;
    border-bottom: dashed black;

    display: flex;
    align-items: center;
    justify-content: center;
}

.card_image > img {
    transform: scale(200%);
}

.card_content {
    display: flex;
    flex-direction: column;
    text-align: left;
    padding: 0 30px;
}

.card_content > h2 {
    text-transform: capitalize;
}

.types > span:not(:first-child)::before {
    content: " | ";
}

.details {
    display: flex;
    flex-direction: column;
}
</style>
