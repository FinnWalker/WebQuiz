<template>
  <div id="response-5-n">
    <p>
      Wrong answer.<br><br>
      Trucks need more room to turn than cars and<br>
      are legally allowed to use 2 lanes to get<br>
      around roundabouts or corners.<br>
      Remember do not overtake turning trucks.
    </p>
    <Button id="roundabout-btn" text="NEXT" identifier="1" @darkness.once=next />
    <img src="../../../assets/img/roundabout.gif" />
  </div>
</template>

<script>
import Button from "../../reusable/Button";
import Velocity from "velocity-animate";

export default {
  name: "Response5T",
  components: {
    Button
  },
  methods: {
    next() {
      this.$emit("next");
    }
  },
  mounted() {
    setTimeout(() => {
      Velocity(document.getElementById('roundabout-btn'), {opacity: 1}, {duration: 1000, complete: () => {document.getElementById('roundabout-btn').style.pointerEvents = 'all'}});
    },5000);
  }
};
</script>

<style scoped>
#roundabout-btn {
  margin-bottom: 2.5%;
  pointer-events: none;
  opacity: 0;
}
p {
  margin-top: 3%;
}
img {
  display: block;
  margin: auto;
  width: 55%;
}
</style>
