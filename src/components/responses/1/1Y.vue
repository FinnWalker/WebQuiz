<template>
  <div id="response-1-y">
    <p>
      Great thinking.<br /><br />It's 85 metres, which is more than the length
      of 7 buses.<br />So don't cut into the space truck drivers leave in front
      of them-<br />they need that space to stop safely.
    </p>
    <img src="../../../assets/img/TruckTrain.png" >
    <Button text="NEXT" identifier="1" @darkness.once=next />
  </div>
</template>

<script>
import Button from "../../reusable/Button";

export default {
  name: "Response1Y",
  components: {
    Button
  },
  methods: {
    next() {
      this.$emit("next");
    }
  }
};
</script>

<style scoped>
img {
  width: 80%;
  display: block;
  margin: 7% auto;
}
</style>
