<template>
  <div id="intro">
    <div id="intro-text">
      Welcome to the <span style="color: white">Safe</span><span style="color: grey">T</span><span style="color: #00ff00">360</span> quiz.
      <br><br>
      Let'stest your knowledge of sharing<br>
      the road safely with trucks.
      <br><br>
      You have 20 seconds to answer each question.
      <br>
      Good luck.
    </div>
    <Button id="next" text="NEXT" identifier="1" @darkness="darkness" />
  </div>
</template>

<script>
import Button from "./reusable/Button";

export default {
  name: "Intro",
  components: {
    Button
  },
  methods: {
    darkness() {
      this.$emit("darkness");
    }
  }
};
</script>

<style scoped>
#intro {
  position: relative;
  height: 100%;
}
#intro-text {
  font-size: 2.5vw;
  line-height: 3.5vw;
  color: rgb(224, 224, 224);
  font-family: light;
  margin: auto;
  margin-top: 10%; 
}
#next {
  margin: auto;
  margin-top: 8%;
}

@media (min-aspect-ratio: 16/9) {
  #intro-text {
    font-size: 4.44444444375vh;
    line-height: 6.22222222125vh;
  }
}
</style>
