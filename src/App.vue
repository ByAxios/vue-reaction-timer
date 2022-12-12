<template>
  <div>

    <header>
      <div class="title">
        <div class="scorlar">
          <h3>Old Scores</h3>
        <ul class="oldScores" v-for="scores in oldScores">
          <li>
            {{ scores }}
          </li>
        </ul>
        </div>
        <h1>Reaction Timer Game</h1>
        <button v-if="!isStarted" @click="startGame()">Tap To Play</button>
      </div>
    </header>

    <section class="gameArea">
      <div v-if="showScore" class="result">
        <h2>{{ score }} ms</h2>
      </div>
      <div v-if="canShowBox" @click="clickBox()"
        :style="{ top: locations.top, left: locations.left }"
        class="box">
        <h1>🖐️</h1>
      </div>
    </section>

  </div>
</template>


<script setup>
import { ref } from "vue"

const isStarted = ref(false)
const canShowBox = ref(false)
const showScore = ref(false)
const score = ref(0)
const delay = ref(null)
const oldScores = ref([])
const locations = ref({ top: 0, left: 0 })
const randomDelay = () => { return 2000 + Math.random() * 2000 }


const startGame = () => {
  locations.value.top = Math.floor(Math.random() * 700 + 50) +"px"
  locations.value.left = Math.floor(Math.random() * 1600 + 50)+"px"
  console.log(locations.value.left);
  console.log(randomDelay());

  isStarted.value = true;
  showScore.value = false;
  score.value = 0
  setTimeout(() => {
    canShowBox.value = true;

    delay.value = setInterval(() => {
      score.value += 10
    }, 10);

  }, randomDelay());

}


const clickBox = () => {
  clearInterval(delay.value)
  isStarted.value = false;
  canShowBox.value = false
  showScore.value = true
  console.log("skor " + score.value);


  oldScores.value.push(score.value)
}

</script>

<style scoped>
header {
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}



.gameArea .box {
  margin-top: 25px;
  
  width: 50px;
  height: 50px;
  position: absolute;
  text-align: center;
  cursor: pointer;
}

.box h1 {
  font-size: 70px;
  padding: 50px;
}

button {
  padding: 10px 15px;
  outline: none;
  border: none;
  cursor: pointer;
  border-radius: 15px;
  background-color: #6140a6;
  color: white;
  font-weight: bold;
}

button:hover {
  background-color: #3d1c85;

}

.scorlar{
  display: flex;
}
.scorlar p{
  margin-left:  5px;
}
</style>