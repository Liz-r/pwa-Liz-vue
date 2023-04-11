<template>
    <div v-if="onLine()">
        <h1>Characters</h1>
        <input type="text" v-model="search" placeholder="Search">
        <div class="content">
            <div class="content-characters" v-for="character in filterSearch" :key="character.id">
                <div class="character">
                    <img :src="character.image" alt="">
                    <div class="info-character">
                        <h2> {{ character.name }}</h2>
                        <h4> {{ character.species }}</h4>
                        <h4> {{ character.status }}</h4>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div v-else>
        <h1>Characters</h1>
        <input type="text" v-model="search" placeholder="OFFLINE" disabled>
        <div class="content">
            <div v-for="(character, idx) in 20 " :key="idx">
                <div class="character">
                    <img src="../assets/img/offline.jpeg" alt="">
                    <div class="info-character">
                        <h2>No info</h2>
                        <h4>Connect</h4>
                        <h4>To Internet</h4>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'

export default {
    name: 'app',
    components: {
    },
    data() {
        return {
            search: '',
            characters: []
        }
    },
    mounted() {
        this.getTodos();
    },
    methods: {
        getTodos() {
            axios
                .get('https://rickandmortyapi.com/api/character/')
                .then(res => {
                    (this.characters = res.data.results)
                })
                .catch(e => {
                    console.log(e)
                })
        },

        onLine() {
            return window.navigator.onLine;
        },
    },
    computed: {
        filterSearch() {
            return this.characters.filter((character) => {
                return character.name.toLowerCase().includes(this.search.toLowerCase())
            })
        }
    },

}
</script>
 
 
<style >
body {
    background-color: #002128;
}

.content {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr;
    gap: 30px 30px;
    width: 80%;
    margin: 0 auto;
}

.content-characters {
    background: #82ffcd;
    padding: 1rem;
    border-radius: 1rem;
}

.content-characters:hover {
    background: #d7f8eb;
}

.character {
    display: flex;
    justify-content: center;
    align-items: center;
}

.info-character {
    display: table-column;
    justify-content: center;
    margin: 0 auto;
}

img {
    height: 50%;
    width: 50%;
    border-radius: 1rem;
}

h1 {
    font-size: 48px;
    color: #82ffcd;
}

h2 {
    font-weight: 100;
    font-size: 1.2rem;
    padding: 1rem;
    background: #82ffcd;
    border-radius: 0.8rem;
    margin: 1rem;
}

h4 {
    margin: 1rem;
    color: #ffffff;
    background: #22245b;
    border-radius: 0.4rem;
    font-weight: 100;
    padding: 0.2rem;
}

input {
    text-align: center;
    background: #82ffcd;
    outline: none;
    border: 0;
    width: 300px;
    margin: 1rem;
    padding: 1rem;
    color: white;
    font-weight: 100;
    border-radius: 1rem;
}

@media screen and (max-width: 918px) {
    .content {
        grid-template-columns: 1fr 1fr;
    }

    .character {
        display: flex;
        align-items: center;
    }

    h2 {
        font-size: 1rem;
    }
}

@media screen and (max-width: 540px) {
    .content {
        width: 90%;
        grid-template-columns: 1fr;
    }

    .character {
        display: flex;
        align-items: center;
    }
}
</style>