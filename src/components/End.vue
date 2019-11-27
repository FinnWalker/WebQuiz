<template>
  <div id="end">
    <img id="logo" src="../assets/img/SafeT360_Logo.png" />
    <Border
      padding="3"
      width="50"
      color="white"
      :text="message"
      :secondText="message2"
      font="beon"
    />
    <p>Remember to play it safe on the road.</p>
    <Button
      id="play"
      text="PLAY"
      text2="AGAIN"
      identifier="1"
      @darkness="darkness"
    />
  </div>
</template>

<script>
import Border from "./reusable/Border";
import Button from "./reusable/Button";

export default {
  name: "End",
  components: {
    Border,
    Button
  },
  props: ["score"],
  data: function() {
    return {
      message: "",
      message2: ""
    };
  },
  methods: {
    darkness() {
      this.$emit("darkness");
    }
  },
  mounted() {
    //document.getElementById('ambient-clip').volume = 1;
    document.getElementById('ambient-clip').play();
    if (this.$props.score < 5) {
      this.message = "SO, YOU SCORED " + this.$props.score + "/8";
      this.message2 = "LEARN MORE AT SAFET360.COM.AU";
    } else {
      this.message = "WELL PLAYED";
      this.message2 = "YOU SCORED " + this.score + "/8";
    }
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
  width: 20%;
  margin-top: 10%;
  margin-bottom: 5%;
}
#play {
  margin: auto;
}
p {
  margin: 5%;
}
</style>
