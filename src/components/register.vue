<template>
    <div>
        <div v-if="number == null && lockReg">
            <form @submit.prevent="submit" >
                <input type="text" 
                    :onchange="countPlayers" 
                    placeholder="Введите количество игроков">
            </form>
        </div>
        <div v-if="number !== null && lockReg">
            <h2>Player {{id}}</h2>
            <hr/>
            <form @submit.prevent="submit">
                <input type="text" 
                    :onchange="createdPlayers" 
                    placeholder="Введите имя">
            </form>
        </div>
        <div v-if="object !== null && lockReg">
            <h2 class="qwe" @click="startSavedGame">Продолжить игру <span :key="c" v-for="c in object">{{c.name}}&nbsp;</span></h2>
        </div>
        <playzone v-if='!lockReg' :players="players"></playzone>
    </div>
</template>


<script>

import playzone from './playzone'

export default {
    name: 'registration',
    data() {
        return {
            lockReg: true,
            number: null,
            players: [],
            id: 1,
            object: JSON.parse (localStorage.getItem ('Saved game'))
        }
    },
    methods: {
        startSavedGame: function() {
            this.players = this.object
            this.lockReg = false
        },
        countPlayers: function(event) {
            this.number = event.target.value
            console.log(this.number)
            console.log(this.object)
            console.log(this.players)
        },
        createdPlayers: function (event) {
            if (this.players.length <= this.number) {
                this.players.push({
                    id: this.id,
                    name: event.target.value,
                    score: 0
                })
                this.id++
                event.target.value = ''
                if((this.id - 1) == this.number) {
                    localStorage.setItem ('Saved game', JSON.stringify(this.players))
                    this.lockReg = false
                }
            }
        }
    },
    components: {
        playzone
    }
    
}
</script>
