<template>
  <div id="response-3-n">
    <p>
      A nice try, but a truck has 4 blind spots.<br />Avoid driving in a truck's blind spots as the truck driver cannot see you.
    </p>
    <img src="../../../assets/img/AllBlindspots.jpg" >
    <Button text="NEXT" identifier="1" @darkness.once=next />
  </div>
</template>

<script>
import Button from "../../reusable/Button";

export default {
  name: "Response1T",
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
  width: 55%;
  display: block;
  margin: 4% auto;
}
</style>
