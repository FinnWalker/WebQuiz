<template>
  <div id="response-6-t">
    <p>
      Whoops, you ran out of time.<br><br>
      Trucks are legally allowed to use 2 lanes to turn a corner.<br>
      Always remember: trucks need more room to get around corners.<br>
      Remember do not overtake turning trucks.
    </p>
    <Button id="roundabout-btn" text="NEXT" identifier="1" @darkness.once=next />
    <img src="../../../assets/img/turn.gif" />
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
  opacity: 0;
  pointer-events: none;
}
p {
  margin-top: 3%;
}
img {
  display: block;
  margin: auto;
  width:46.5%;
}
</style>
