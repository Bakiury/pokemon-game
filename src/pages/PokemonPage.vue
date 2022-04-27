<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>

    <div v-else class="myBox">
        <h1>¿Quién es este pokemon?</h1>

        <PokeImage :pokeId="pokemon.id" :showPoke="showPokemon" />
        <PokeOptions :pokemons="pokemonArr" @selection="checkAnswer($event)" />

        <template v-if="showAnswer">
            <h2
                class="fade-in myMsgWrong"
                :class="{ myMsgCorrect: correctOrWrong }"
            >
                {{ message }}
            </h2>
            <button @click="newGame">Nuevo juego</button>
            <br />
        </template>
    </div>
</template>

<script>
import PokeImage from '@/components/PokeImage'
import PokeOptions from '@/components/PokeOptions'

import getPokemonOptions from '@/helpers/getPokemonOptions'

export default {
    components: {
        PokeImage,
        PokeOptions,
    },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: '',
            correctOrWrong: false,
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor(Math.random() * 4)
            this.pokemon = this.pokemonArr[rndInt]
        },
        checkAnswer(selectedId) {
            this.showPokemon = true
            this.showAnswer = true

            if (selectedId === this.pokemon.id) {
                this.correctOrWrong = true
                this.message = `Correcto, ${this.pokemon.name}`
            } else {
                this.correctOrWrong = false
                this.message = `Oops, era ${this.pokemon.name}`
            }
        },
        newGame() {
            this.showPokemon = false
            this.showAnswer = false
            this.pokemonArr = []
            this.pokemon = null
            this.mixPokemonArray()
        },
    },
    mounted() {
        this.mixPokemonArray()
    },
}
</script>

<style scoped>
.myBox {
    background: #74b9ff;
    border-radius: 10px;
    padding: 20px;
    position: absolute;
    width: 500px;
    transform: translateX(-50%);
    left: 50%;
    box-shadow: 0 0 5px 2px #333333;
}

button {
    padding: 10px;
    font-size: 17px;
    font-weight: bold;
    width: 260px;
    border-radius: 10px;
    border: 2px solid #34495e;
    background: #34495e;
    color: #ffffff;
    cursor: pointer;
}

button:hover {
    border: 2px solid #2c3e50;
    background: #2c3e50;
    transition: ease all 0.3s;
}

.myMsgWrong {
    color: #b33939;
    font-weight: bold;
}

.myMsgCorrect {
    color: #218c74;
    font-weight: bold;
}
</style>
