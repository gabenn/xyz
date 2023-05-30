<template>
    <div>
        <div>
            <input
                type="text"
                id="name"
                placeholder="Your favourite pokemon"
                v-model="id"
            />
            <input type="button" value="Search" @click="getPokemon(id)" />
        </div>
        {{ name }}
        <img :src="src" alt="" />
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
    name: "searchView",
    data() {
        return {
            id: "squirtle",
            name: "",
            src: "",
        };
    },
    components: {},
    methods: {
        getPokemon(id: String): void {
            const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
            fetch(url)
                .then((res) => res.json())
                .then((res) => {
                    this.name = res.name;
                    this.src = res.sprites.front_default;
                });
        },
    },
    mounted() {
        this.getPokemon("squirtle");
    },
});
</script>
