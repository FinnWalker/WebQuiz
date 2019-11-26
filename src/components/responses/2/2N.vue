<template>
  <div id="response-2-n">
    <p>
      Wrong answer.<br /><br />It's 183 metres, which is more than the length
      of a football field.<br />Trucks neeed more distance than cars to stop.<br>Give truck drivers the space they need to stop safely.
    </p>
    <img src="../../../assets/img/field.jpg" >
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
  width: 35%;
  display: block;
  margin: 3% auto;
}
</style>
