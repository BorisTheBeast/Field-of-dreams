<template>
    <div>
        <div class="custom">
            <questionZone  :drumScore="drumScore" :players="players"></questionZone>
            <button v-bind:class="{'disabled': rotating}" @click='rotateDrum'>Вращайте барабан</button>
            <div>{{drumScore}} очков на барабане</div>
            <img class="rot" src="./img/circle.png" alt="альтернативный текст">
            <i class="up"></i>
        </div>
        <playerStats :players="players"></playerStats>
    </div>
</template>

<script>

// import drum from './drum'
import questionZone from './questionzone'
import playerStats from './playerStats'


export default {
    name: 'playzone',
    data() {
        return {
            rotating: false,
            angle: 0,
            drumResultAngle: 0,
            drumScores: [500, 0, 0, 900, 400, 'х2', 800, 600, 300, 100, 1000, 'х2', 700, 'x3', 200, 300],
            drumScore: "",
            canClick: false
        }
    },
    props: ['players', 'questions'],
    components: {
        questionZone,
        playerStats
    },
    methods: {
        rotateDrum: function () {
            if (this.rotating) return;
            this.rotating = true;

            const drum = document.querySelector('.rot')
            let timeout = (Math.floor(Math.random() * (10000 - 5000) + 5000))/10
            let parameter = 0.5
            let degree =  this.angle
            let animator = () => {
                degree = degree + (360 * (1 / parameter)) * (timeout / 1000)

                drum.style.cssText = `
                    transform: rotate(${degree}deg);
                    transition-duration: ${(timeout / 1000)}s;
                `
                parameter += 0.2
                if (parameter > 3) {
                    this.angle = degree
                    this.drumResultAngle = Math.round((this.angle % 360)/ 22.5)
                    this.drumScore = this.drumScores[this.drumScores.length - this.drumResultAngle - 1]
                    this.canClick = true
                } else {
                    setTimeout(animator, timeout)
                }
            }
            animator();
        }
    }
}


</script>


<style>
.custom {
    display: block;
}

playerStats {
    text-align: center;
}

img.rot {
    width: 300px;
    transition-timing-function: linear;
}

.disabled {
    opacity: 0.3;
    background-color: red;
}
i {
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 10px;
}
.up {
    transform: rotate(-135deg);
    -webkit-transform: rotate(-135deg);
}


</style>