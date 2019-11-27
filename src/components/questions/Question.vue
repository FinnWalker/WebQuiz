<template>
  <div id="question">
    <audio id="correct-clip">
      <source src="../../assets/audio/SelectSound.wav" type="audio/wav" />
    </audio>
    <audio id="incorrect-clip">
      <source src="../../assets/audio/SelectSoundWrong.wav" type="audio/wav" />
    </audio>
    <div id="darkness-2" />
    <div v-if="state === 'active'">
      <Timer id="timer" @timeout="timeout" />
      <h2>QUESTION {{ question.number }} OF 8</h2>
      <h1>{{ question.title }}</h1>
      <Border
        :width="question.width !== undefined ? question.width : 55"
        margin="3"
        color="#00ff00"
        :text="question.text"
        font="light"
      />
      <div id="sign-div" v-if="question.number === 4">
        <img src="../../assets/img/Sign.jpg" id="sign" />
      </div>
      <div id="roundabout-div" v-if="question.number === 5">
        <Answer
          class="roundabout-answer"
          :identifier="question.answers[0].index"
          :text="question.answers[0].text"
          @answerQuestion="answerQuestion"
          :type="question.answers[0].type"
        />
        <img src="../../assets/img/roundabout.png" id="roundabout" />
        <Answer
          class="roundabout-answer"
          :identifier="question.answers[1].index"
          :text="question.answers[1].text"
          @answerQuestion="answerQuestion"
          :type="question.answers[1].type"
        />
      </div>

      <div v-if="question.number === 6">
        <Answer
          class="roundabout-answer"
          :identifier="question.answers[0].index"
          :text="question.answers[0].text"
          @answerQuestion="answerQuestion"
          :type="question.answers[0].type"
        />
        <img src="../../assets/img/corner.png" id="corner" />
        <Answer
          class="roundabout-answer"
          :identifier="question.answers[1].index"
          :text="question.answers[1].text"
          @answerQuestion="answerQuestion"
          :type="question.answers[1].type"
        />
      </div>

      <div
        v-if="
          question.number !== 3 &&
            question.number !== 5 &&
            question.number !== 6
        "
        id="answers"
      >
        <Answer
          class="answer-box"
          v-for="answer in question.answers"
          :key="answer.index"
          :identifier="answer.index"
          :text="answer.text"
          @answerQuestion="answerQuestion"
          :type="answer.type"
        />
      </div>
      <div v-if="question.number === 3" id="answers">
        <Blindspots @answerQuestion="answerQuestion" />
      </div>
    </div>
    <div v-if="state !== 'active'">
      <Response :state="state" :questionNumber="question.number" @next="next" />
    </div>
  </div>
</template>

<script>
import Timer from "../reusable/Timer";
import Border from "../reusable/Border";
import Answer from "../reusable/Answer";
import Response from "../responses/Response";
import Blindspots from "./Blindspots";
import Velocity from "velocity-animate";

export default {
  name: "Question",
  props: ["question"],
  components: {
    Timer,
    Border,
    Answer,
    Response,
    Blindspots
  },
  data: function() {
    return {
      state: "active",
      transitioning: false
    };
  },
  methods: {
    playSelect() {
      document.getElementById("correct-clip").pause();
      document.getElementById("correct-clip").currentTime = 0;
      document.getElementById("correct-clip").play();
    },
    
    timeout() {
      if (!this.transitioning) {
        this.answerQuestion("timeout");
      }
    },
    next() {
      this.playSelect();
      if (this.$props.question.number === 8) {
        this.$emit("next");
        return;
      }
      document.getElementById("question").style.pointerEvents = "none";
      Velocity(
        document.getElementById("darkness-2"),
        { opacity: 1 },
        {
          duration: 1000,
          complete: () => {
            document.getElementById("question").style.pointerEvents = "all";
            this.$emit("next");
            this.state = "active";

            Velocity(
              document.getElementById("darkness-2"),
              { opacity: 0 },
              { duration: 1000 }
            );
          }
        }
      );
    },
    answerQuestion(type) {
      document.getElementById("timer-clip").pause();
      if (type === "correct" && this.question.number !== 3) {
        this.playSelect();
      } else if (type === "incorrect" && this.question.number !== 3) {
        document.getElementById("incorrect-clip").play();
      }
      this.transitioning = true;
      document.getElementById("question").style.pointerEvents = "none";
      Velocity(
        document.getElementById("darkness-2"),
        { opacity: 1 },
        {
          duration: 1000,
          complete: () => {
            this.transitioning = false;
            if (type === "correct") {
              this.state = "correct";
              this.$emit("correct");
            } else if (type === "incorrect") {
              this.state = "incorrect";
            } else {
              this.state = "timeout";
            }
            document.getElementById("question").style.pointerEvents = "all";
            Velocity(
              document.getElementById("darkness-2"),
              { opacity: 0 },
              { duration: 1000 }
            );
          }
        }
      );
    }
  },
  mounted() {
    //document.getElementById('ambient-clip').volume = 0.25;
    document.getElementById("ambient-clip").pause();
  }
};
</script>

<style scoped>
h1 {
  font-family: regular;
  font-size: 2.25vw;
  margin: 0;
  color: white;
}
h2 {
  font-family: light;
  color: rgb(75, 75, 75);
  font-size: 1.6vw;
  margin: 1%;
}

#timer {
  margin-top: 1.25%;
  margin-bottom: 3.5%;
}
#border {
  margin-top: 2.5%;
}
#answers {
  margin: auto;
  text-align: center;
  width: 100%;
}
#sign-div {
  position: relative;
  width: 100%;
  display: block;
  margin-top: 3%;
  margin-bottom: 8%;
}
#roundabout-div {
  margin-top: 3%;
}

#sign {
  position: absolute;
  left: 0;
  right: 0;
  margin: auto;
  width: 12%;
}
#roundabout {
  display: inline-block;
  width: 45%;
}
#corner {
  display: inline-block;
  width: 50%;
}
.answer-box {
  margin: 8% 10%;
}
.roundabout-answer {
  position: relative;
  top: -12vw;
  margin: 0;
}
@media (min-aspect-ratio: 16/9) {
  h1 {
    font-size: 4vh;
  }
  h2 {
    font-size: 2.844444444vh;
  }
  .roundabout-answer {
    top: -21.3333333333vh;
  }
}
#darkness-2 {
  pointer-events: none;
  position: absolute;
  width: 100%;
  height: 100%;
  background: black;
  z-index: 2;
  opacity: 0;
}
</style>
