<template>
    <nav>
        <router-link to="/">Home</router-link>
        <router-link to="/search">Search</router-link>
    </nav>
    <router-view />
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "app",
    methods: {
        test: function (n = 20): number {
            return n;
        },
    },
    mounted() {},
});
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

nav {
    padding: 30px;
}

nav a:not(:first-child)::before {
    content: " | ";
}

nav a {
    font-weight: bold;
    color: #2c3e50;
    text-decoration: none;
}

nav a.router-link-exact-active {
    color: #42b983;
}
nav a.router-link-exact-active::before {
    color: #2c3e50;
}
</style>
