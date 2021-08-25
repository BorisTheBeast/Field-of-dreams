<template>
    <div class="questionBlock">
        <button @click="setQuestion">Начать игру</button>
        <h2>{{ settedQuestion.question }}</h2>
    </div>
    <div class="btnBlock">
        <div class="blackWindows" v-for="(c, i) in settedQuestion.answer" v-bind:key="i"><span v-if="userAnswer && userAnswer.indexOf(c) != -1">{{ c }}</span></div>
    </div>
    <h2 class='currentPlayer'>Игрок {{players[playerId].name}} вращайте барабан</h2>
    <div class="keys">
        <div class="btnBlock">
            <button class="btnQ">клавиатура</button>
        </div>
        <img class='yakubReact' :src="require(`@/components/img/${yakubImg}.jpg`)">
        <div class="keys">
            <div class="keyboard">
            <button class="keyboardBtn"  v-for="b in keyboard" v-bind:key="b" @click="userChoice">{{ b }}</button>
            </div>
        </div>
    </div>
        
</template>

<script>

export default {
    name: 'questionzone',
    props: ['players', 'drumScore'],
    data() {
        return {
            questions: [
                {id: 1, question: 'Как у западных и южных славян назывались селение, деревня, курень?', answer: 'жупа'},
                {id: 2, question: 'Что использовали в Китае для глажки белья вместо утюга?', answer: 'сковорода'},
                {id: 3, question: 'В Австралии на парковках возле некоторых торговых центров по ночам и вечерам включают классическую музыку, чтобы отпугнуть кого-то. Кого?', answer: 'подросток'},
                {id: 4, question: 'В словаре Владимира Ивановича Даля встречается старинное название барометра. Какое?', answer: 'буревестник'},
                {id: 5, question: 'Английский писатель Киплинг говорил: «Женская интуиция намного точнее, чем мужская...»', answer: 'уверенность'},
                {id: 6, question: 'Герцогиня Англии XVIII века Сара Черчилль говорила: "Вы молоды, если вы еще способны..."', answer: 'разочаровываться'},
                {id: 7, question: 'Первый подобный музей появился в Париже до 1975 года. Экскурсии по нему проводились на лодке. Сейчас туристы осматривают его экспонаты со специальных решеток и пандусов. О каком музее идет речь?', answer: 'канализация'},
            ],
            settedQuestion: [],
            userAnswer: [''],
            keyboard: [],
            playerId: 0,
            yakubImg: 'rotate'
        }
    },
    methods: {
        setQuestion: function() {
            this.settedQuestion = this.questions[Math.floor( Math.random()*(Object.keys(this.questions).length))]
            this.userAnswer = [''],
            this.setKeyboard()
        },
        setKeyboard: function() {
            if(!this.keyboard.length) {
                for(let i = 1072; i <= 1103; i++) {
                    this.keyboard.push(String.fromCharCode(i))
                }
            }
        },
        userChoice: function(event) {
            if(this.$parent.canClick) {
                for(let i = 0; i <= this.settedQuestion.answer.length; i++) {
                    if(event.target.textContent == this.settedQuestion.answer[i]) {
                        this.userAnswer.push(event.target.textContent)
                        console.log(this.drumScore)
                        if(this.drumScore == 'х2') {
                            this.players[this.playerId].score *= 2
                        } else if (this.drumScore == 'х3') {
                            this.players[this.playerId].score *= 3
                        } else {
                            this.players[this.playerId].score += this.drumScore
                        }
                        this.yakubImg = 'wow'
                        setTimeout(() => this.yakubImg = 'rotate', 3000)
                        if((this.userAnswer.length - 1) == this.settedQuestion.answer.length) {
                            document.querySelector('.currentPlayer').textContent = `${this.players[this.playerId].name} КРАСИВЫЙ!!!!`
                            this.yakubImg = 'wow'
                        }
                        localStorage.setItem ('Saved game', JSON.stringify(this.players));
                        break
                    } else if (i == this.settedQuestion.answer.length && event.target.textContent !== this.settedQuestion.answer[i]) {
                        if(this.playerId == this.players.length - 1) {
                            this.playerId = 0
                        } else {
                        this.playerId++
                        this.yakubImg = 'lol'
                        setTimeout(() => this.yakubImg = 'rotate', 3000)
                        }
                        break
                    }
                }
                this.$parent.canClick = !this.$parent.canClick
                this.$parent.rotating = false
            }
        }
    }
}


</script>


<style>
    .keys {
        float: right;
        text-align: end;
    }
    .btnQ {
        display: inline;
    }
    .btnBlock {
        text-align: end;
    }
    .blackWindows {
        position: relative;
        display: inline-block;
        width: 30px;
        height: 30px;
        border: 3px solid black;
        padding: 8px;
        margin: 2px;
        background-color: black;
    }
    .blackWindows span {
        display: inline-block;
        position: absolute;
        left: 35%;
        top: 10%;
    }
    .keyboard {
        display: inline-block;
        margin:0px auto 0px auto;
        width: 120px;
    }
    .keyboardBtn {
        display: inline;
        width: 30px;
        border: 2px solid white;
        background-color: black;
        color: white;
    }
    .yakubReact {
        max-width: 300px;
        max-height: 230px;
    }
    .questionBlock {
        height: 180px
    }
</style>