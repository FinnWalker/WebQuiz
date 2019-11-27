<template>
  <div id="home">
    <img id="logo" src="../assets/img/SafeT360_Logo.png" />
    <Border padding=1 width="45" color="white" :text="slogan" font="beon" />
    <Button id="play" text="PLAY" identifier="1" @darkness="darkness" />
  </div>
</template>

<script>
import Border from "./reusable/Border";
import Button from "./reusable/Button";
import Velocity from "velocity-animate";

export default {
  name: "Home",
  components: {
    Border,
    Button
  },
  data: function() {
    return {
      interval: null,
      slogan: "ROAD SAFETY FROM EVERY ANGLE"
    };
  },
  methods: {
    darkness() {
      document.getElementById('ambient-clip').play();
      this.$emit("darkness");
    }
  },
  mounted() {
    this.interval = setInterval(() => {
      Velocity(
        document.getElementById("text"),
        { opacity: 0 },
        {
          duration: 1000,
          complete: () => {
            if (this.slogan === "TAKE THE QUIZ") {
              this.slogan = "ROAD SAFETY FROM EVERY ANGLE";
            } else {
              this.slogan = "TAKE THE QUIZ";
            }
            Velocity(
              document.getElementById("text"),
              { opacity: 1 },
              {
                duration: 1000
              }
            );
          }
        }
      );
    }, 4000);
  },
  destroyed() {
    clearInterval(this.interval);
  }
};
</script>

<style scoped>
#home {
  position: relative;
  height: 100%;
}
#logo {
  position: relative;
  width: 45%;
  margin-top: 16%;
  margin-bottom: 3.4%;
}
#play {
  margin: auto;
  margin-top: 4.8%;
}
</style>
