<template>
    <section class="options-container">
        <div
            v-for="pokemon in pokemons"
            :key="pokemon.id"
            @click="$emit('selection', pokemon.id)"
            class="options"
        >
            {{ pokemon.name }}
        </div>
    </section>
</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true,
        },
    },
}
</script>

<style scoped>
.options {
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    padding: 8px;
    width: 250px;
}

.options:hover {
    background-color: rgba(0, 0, 0, 0.3);
    color: #ffffff;
}

.options-container {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
}
</style>
