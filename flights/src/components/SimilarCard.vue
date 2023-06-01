<template>
    <div class="card">
        <span>{{ id + 1 }} {{ name }}</span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "similarCard",
    data() {
        return {
            name: this.similar!.pokemon.name,
        };
    },
    props: { similar: Object, id: { type: Number, required: true } },
    mounted() {},
});
</script>

<style scoped>
.card {
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
</style>
