<template>
  <div id="blindspots">
    <audio id="blindspot-clip">
      <source src="../../assets/audio/BlindspotSelect.wav" type="audio/wav" />
    </audio>
    <img id="spots" src="../../assets/img/Blindspots.jpg" />
    <img
      v-if="car_states[2]"
      id="top"
      src="../../assets/img/TopBlindspot.jpg"
    />
    <img v-if="car_states[3]" id="back" src="../../assets/img/Back.jpg" />
    <img v-if="car_states[5]" id="bottom" src="../../assets/img/Bottom.jpg" />
    <img v-if="car_states[4]" id="front" src="../../assets/img/Front.jpg" />
    <img v-if="car_states[0]" id="car-1" src="../../assets/img/Car.jpg" />
    <img v-if="car_states[1]" id="car-2" src="../../assets/img/Car.jpg" />
    <img v-if="car_states[6]" id="car-3" src="../../assets/img/Car.jpg" />
    <input
      id="box-1"
      @change="checkAnswer(0)"
      class="checkbox-wrong-answer"
      type="checkbox"
    />
    <input
      id="box-2"
      @change="checkAnswer(1)"
      class="checkbox-wrong-answer"
      type="checkbox"
    />
    <input
      id="box-3"
      @change="checkAnswer(2)"
      class="checkbox-answer"
      type="checkbox"
    />
    <input
      id="box-4"
      @change="checkAnswer(3)"
      class="checkbox-answer"
      type="checkbox"
    />
    <input
      id="box-5"
      @change="checkAnswer(4)"
      class="checkbox-answer"
      type="checkbox"
    />
    <input
      id="box-6"
      @change="checkAnswer(5)"
      class="checkbox-answer"
      type="checkbox"
    />
    <input
      id="box-7"
      @change="checkAnswer(6)"
      class="checkbox-wrong-answer"
      type="checkbox"
    />
  </div>
</template>

<script>
export default {
  name: "Blindspots",
  data: function() {
    return {
      checkboxAnswers: [],
      checkboxWrongAnswers: [],
      car_states: {
        0: false,
        1: false,
        2: false,
        3: false,
        4: false,
        5: false,
        6: false
      }
    };
  },
  methods: {
    checkAnswer(car) {
      document.getElementById('blindspot-clip').pause();
      document.getElementById('blindspot-clip').currentTime = 0;
      document.getElementById('blindspot-clip').play();
      this.car_states[car] = !this.car_states[car];
      this.$emit("blindspot");
      let count = 0;
      for (let answer of this.checkboxAnswers) {
        if (answer.checked) count++;
      }
      if (count === 4) {
        this.$emit("answerQuestion", "correct");
      } else {
        for (const answer of this.checkboxWrongAnswers) {
          if (answer.checked) {
            count++;
          }
        }
        if (count === 4) {
          this.$emit("answerQuestion", "incorrect");
        }
      }
    }
  },
  mounted() {
    this.checkboxAnswers = document.getElementsByClassName("checkbox-answer");
    this.checkboxWrongAnswers = document.getElementsByClassName(
      "checkbox-wrong-answer"
    );
  }
};
</script>

<style scoped>
#blindspots {
  position: relative;
  width: 100%;
  height: 28.125vw;
}
@media (min-aspect-ratio: 16/9) {
  #blindspots {
    height: 50vh;
  }
}
#spots {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  width: 58%;
  left: 0;
  right: 0;
}
#top {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 0.2%;
  width: 33.17%;
  left: 2.65%;
  right: 0;
  opacity: 1;
}
#back {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 50%;
  width: 16.8%;
  left: -38.5%;
  right: 0;
  opacity: 1;
}
#bottom {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 69.5%;
  width: 13.7%;
  left: 11.2%;
  right: 0;
  opacity: 1;
}
#front {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 50%;
  width: 15%;
  left: 49.5%;
  right: 0;
  opacity: 1;
}
#car-1 {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 0%;
  width: 9.5%;
  left: 46.85%;
  right: 0;
  opacity: 1;
}
#car-2 {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 24%;
  width: 9.5%;
  left: -41.2%;
  right: 0;
  opacity: 1;
}
#car-3 {
  position: absolute;
  margin: auto;
  margin-top: 1%;
  top: 76.5%;
  width: 9.5%;
  left: 45.9%;
  right: 0;
  opacity: 1;
}

input[type="checkbox"] {
  -webkit-appearance: none;
  outline: none;
  width: 9.75%;
  height: 15.5%;
  margin: auto;
  margin-top: 1%;
  left: 0;
  right: 0;
  border-radius: 15%;
  position: absolute;
  background: rgba(255, 255, 255, 0);
}

#box-1 {
  left: 46.85%;
}
#box-2 {
  top: 24%;
  left: -41.25%;
}
#box-3 {
  top: 23.9%;
  left: 8.05%;
}
#box-4 {
  top: 50.04%;
  left: -34%;
}
#box-5 {
  top: 50.04%;
  left: 44%;
}
#box-6 {
  top: 76.5%;
  left: 7.35%;
}
#box-7 {
  top: 76.5%;
  left: 45.9%;
}
</style>
