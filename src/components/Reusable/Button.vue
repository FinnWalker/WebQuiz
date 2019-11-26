<template>
  <div class="button-container" @click.once="test">
    <div :id="identifier" class="button">
      <div class="text" :id="identifier + 'text'">{{ text }}<br>{{ text2 }}</div>
    </div>
  </div>
</template>

<script>
import Velocity from "velocity-animate";

export default {
  name: "Button",
  props: ["text", "identifier", "text2"],
  methods: {
    test() {
      this.$emit("darkness");
      Velocity(
        document.getElementById(this.$props.identifier),
        { width: "85%", height: "85%", opacity: 0.5 },
        { duration: 200 }
      );
      Velocity(
        document.getElementById(this.$props.identifier + "text"),
        { opacity: 0 },
        { duration: 600 }
      );
      Velocity(
        document.getElementById(this.$props.identifier),
        { width: "130%", height: "130%", opacity: 0 },
        { duration: 600 }
      );
    }
  }
};
</script>

<style scoped>
.button-container {
  position: relative;
  width: 5.5vw;
  height: 5.5vw;
  border-radius: 50%;
  display: inline-block;
}
.button {
  pointer-events: none;
  position: absolute;
  left: -50%;
  right: -50%;
  top: -50%;
  bottom: -50%;
  margin: auto;
  width: 100%;
  height: 100%;
  border: 0.2vw solid white;
  border-radius: 50%;
}

.text {
  pointer-events: none;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  height: 100%;
  font-size: 1.575vw;
  font-family: beon;
  color: white;
}

@media (min-aspect-ratio: 16/9) {
  .button {
    border: 0.35555555555vh solid white;
  }
  .button-container {
    width: 9.77777777779vh;
    height: 9.77777777779vh;
  }
  .text {
    font-size: 2.8vh;
  }
}
</style>
