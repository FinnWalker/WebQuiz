<template>
  <div id="response">
    <div v-if="questionNumber === 1">
      <R1Y v-if="state === 'correct'" @next=next />
      <R1N v-if="state === 'incorrect'" @next=next />
      <R1T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 2">
      <R2Y v-if="state === 'correct'" @next=next />
      <R2N v-if="state === 'incorrect'" @next=next />
      <R2T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 3">
      <R3Y v-if="state === 'correct'" @next=next />
      <R3N v-if="state === 'incorrect'" @next=next />
      <R3T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 4">
      <R4Y v-if="state === 'correct'" @next=next />
      <R4N v-if="state === 'incorrect'" @next=next />
      <R4T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 5">
      <R5Y v-if="state === 'correct'" @next=next />
      <R5N v-if="state === 'incorrect'" @next=next />
      <R5T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 6">
      <R6Y v-if="state === 'correct'" @next=next />
      <R6N v-if="state === 'incorrect'" @next=next />
      <R6T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 7">
      <R7Y v-if="state === 'correct'" @next=next />
      <R7N v-if="state === 'incorrect'" @next=next />
      <R7T v-if="state === 'timeout'" @next=next />
    </div>
    <div v-if="questionNumber === 8">
      <R8Y v-if="state === 'correct'" @next=next />
      <R8N v-if="state === 'incorrect'" @next=next />
      <R8T v-if="state === 'timeout'" @next=next />
    </div>
  </div>
</template>

<script>
import R1Y from "./1/1Y";
import R1N from "./1/1N";
import R1T from "./1/1T";
import R2Y from "./2/2Y";
import R2N from "./2/2N";
import R2T from "./2/2T";
import R3Y from "./3/3Y";
import R3N from "./3/3N";
import R3T from "./3/3T";
import R4Y from "./4/4Y";
import R4N from "./4/4N";
import R4T from "./4/4T";
import R5Y from "./5/5Y";
import R5N from "./5/5N";
import R5T from "./5/5T";
import R6Y from "./6/6Y";
import R6N from "./6/6N";
import R6T from "./6/6T";
import R7Y from "./7/7Y";
import R7N from "./7/7N";
import R7T from "./7/7T";
import R8Y from "./8/8Y";
import R8N from "./8/8N";
import R8T from "./8/8T";

export default {
  name: "Response",
  components: {
    R1Y,
    R1N,
    R1T,
    R2Y,
    R2N,
    R2T,
    R3Y,
    R3N,
    R3T,
    R4Y,
    R4N,
    R4T,
    R5Y,
    R5N,
    R5T,
    R6Y,
    R6N,
    R6T,
    R7Y,
    R7N,
    R7T,
    R8Y,
    R8N,
    R8T,
  },
  props: ["state", "questionNumber"],
  methods: {
    next() {
      this.$emit("next");
    }
  }
};
</script>

<style>
p {
  margin-top: 7%;
  color: #00ff00;
  font-family: light;
  font-size: 2.25vw;
  line-height: 3vw;
}

@media (min-aspect-ratio: 16/9) {
  p {
    font-size: 3.99999999938vh;
    line-height: 5.3333333325vh;
  }
}

img {
  position: relative;
}
</style>
