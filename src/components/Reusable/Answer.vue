<template>
  <div id="answer">
    
    <div id="answer-text">{{text}}</div>
    <Button :identifier=identifier @darkness=answerQuestion />
  </div>
</template>

<script>
import Button from "./Button";

export default {
  name: "Answer",
  props: ["identifier", "text", "type"],
  components: {
    Button
  },
  methods: {
    answerQuestion() {
      
      this.$emit("answerQuestion", this.$props.type);
    }
  }
};
</script>

<style scoped>
#answer {
  width: 12%;
  text-align: center;
  display: inline-block;
}
#answer-text {
  font-family: regular;
  color: white;
  font-size: 1.92vw;
  margin: 1%;
  margin-bottom: 20%;
}
@media (min-aspect-ratio: 16/9) {
  #answer-text {
    font-size: 3.4133333328vh;
  }
}
.button {
  background: red;
}
</style>
