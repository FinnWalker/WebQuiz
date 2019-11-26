<template>
  <div id="app">
    <audio id="select-clip">
      <source src="./assets/audio/SelectSound.wav" type="audio/wav" />
    </audio>
    <audio id="ambient-clip" autoplay loop>
      <source src="./assets/audio/ambient.mp3" type="audio/mp3" />
    </audio>
    <div id="background" />
    <div id="darkness" />
    <Home v-if="page === 0" @darkness="darkness" />
    <Intro v-if="page === 1" @darkness="darkness" />
    <Question
      v-if="page === 2 && question < 8"
      :question="questions[question]"
      @next="next"
      @correct="score += 1"
    />
    <End v-if="page === 3" :score="this.score" @darkness="restart" />
  </div>
</template>

<script>
import Home from "./components/Home";
import Intro from "./components/Intro";
import Question from "./components/questions/Question";
import End from "./components/End";
import Velocity from "velocity-animate";

export default {
  name: "app",
  components: {
    Home,
    Intro,
    Question,
    End
  },
  data: function() {
    return {
      score: 0,
      page: 0,
      question: 0,
      questions: [
        {
          number: 1,
          title: "STOPPING DISTANCE",
          text:
            "Travelling at 60 km/h, how much room does a truck need to stop?",
          answers: [
            { index: 1, text: "50 metres", type: "incorrect" },
            { index: 2, text: "85 metres", type: "correct" },
            { index: 3, text: "125 metres", type: "incorrect" }
          ]
        },
        {
          number: 2,
          title: "STOPPING DISTANCE",
          text:
            "Travelling at 100 km/h, how much room does a truck need to stop?",
          answers: [
            { index: 1, text: "67 metres", type: "incorrect" },
            { index: 2, text: "109 metres", type: "incorrect" },
            { index: 3, text: "183 metres", type: "correct" }
          ]
        },
        {
          number: 3,
          title: "BLINDSPOTS",
          text:
            "Where are the 4 main blind spots around this truck? Touch the screen to locate them."
        },
        {
          number: 4,
          title: "TURNING VEHICLE",
          text: "Do you know what this sign means?",
          answers: [
            { index: 1, text: "Yes", type: "correct" },
            { index: 2, text: "No", type: "incorrect" }
          ]
        },
        {
          number: 5,
          title: "TURNING VEHICLE",
          text:
            "Is it safe for the car to pass the truck along the white arrow?",
          answers: [
            { index: 1, text: "Yes", type: "incorrect" },
            { index: 2, text: "No", type: "correct" }
          ],
          width: 75
        },
        {
          number: 6,
          title: "TURNING VEHICLE",
          text:
            "Is this truck legally allowed to use 2 lanes to make this turn?",
          answers: [
            { index: 1, text: "Yes", type: "correct" },
            { index: 2, text: "No", type: "incorrect" }
          ],
          width: 75
        },
        {
          number: 7,
          title: "DRIVER DISTRACTION",
          text:
            "Texting while driving increases your risk of crashing by __ times.",
          answers: [
            { index: 1, text: "2", type: "incorrect" },
            { index: 2, text: "4", type: "incorrect" },
            { index: 3, text: "6", type: "correct" }
          ]
        },
        {
          number: 8,
          title: "DRIVER DISTRACTION",
          text:
            "Young drivers engage in distracting activity every __ minutes while driving?",
          answers: [
            { index: 1, text: "4", type: "incorrect" },
            { index: 2, text: "6", type: "correct" },
            { index: 3, text: "9", type: "incorrect" }
          ]
        }
      ]
    };
  },
  methods: {
    playSelect() {
      document.getElementById('select-clip').pause();
      document.getElementById('select-clip').currentTime = 0;
      document.getElementById('select-clip').play();
    },
    darkness() {
      this.playSelect()
      Velocity(
        document.getElementById("darkness"),
        { opacity: 1 },
        {
          duration: 1000,
          complete: () => {
            this.page = (this.page + 1) % 4;
            document.getElementById("background").style.opacity = "1";
            Velocity(
              document.getElementById("darkness"),
              { opacity: 0 },
              { duration: 1000 }
            );
          }
        }
      );
    },
    lightness() {
      this.playSelect();
      Velocity(
        document.getElementById("darkness"),
        { opacity: 1 },
        {
          duration: 1000,
          complete: () => {
            this.page = (this.page + 1) % 4;
            document.getElementById("background").style.opacity = "0";
            Velocity(
              document.getElementById("darkness"),
              { opacity: 0 },
              { duration: 1000 }
            );
          }
        }
      );
    },
    next() {
      if (this.question + 1 === 8) {
        this.lightness();
      } else {
        this.question += 1;
      }
    },
    restart() {
      Velocity(
        document.getElementById("darkness"),
        { opacity: 1 },
        {
          duration: 1000,
          complete: () => {
            this.page = 0;
            this.score = 0;
            this.question = 0;
            Velocity(
              document.getElementById("darkness"),
              { opacity: 0 },
              { duration: 1000 }
            );
          }
        }
      );
    }
  }
};
</script>

<style>
* {
  user-select: none;
}
@font-face {
  font-family: "beon";
  src: url("./assets/fonts/beon-webfont.ttf");
}
@font-face {
  font-family: "regular";
  src: url("./assets/fonts/Brown-Regular.otf");
}
@font-face {
  font-family: "light";
  src: url("./assets/fonts/Brown-Light.otf");
}
html {
  height: 100%;
}
body {
  margin: 0;
  background: white;
  height: 100%;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100vw;
  height: 56.25vw;
  background: url("./assets/img/stars.png");
  background-size: cover;
  position: absolute;
  left: 0;
  right: 0;
  margin: auto;
  overflow: hidden;
}

@media (min-aspect-ratio: 16/9) {
  #app {
    height: 100vh;
    width: 177.777777778vh;
  }
}

#darkness {
  pointer-events: none;
  position: absolute;
  width: 100%;
  height: 100%;
  background: black;
  z-index: 2;
  opacity: 0;
}
#background {
  pointer-events: none;
  position: absolute;
  width: 100%;
  height: 100%;
  background: black;
  z-index: 0;
  opacity: 0;
}

text {
  text-anchor: middle;
  user-select: none;
  pointer-events: none;
}
h1,
h2,
p,
#answer-text {
  position: relative;
  z-index: 1;
}
,
img {
  z-index: 1;
}
</style>
