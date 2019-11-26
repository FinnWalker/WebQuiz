<template>
  <div id="response-7-t">
    <p>
      Whoops, you ran out of time.<br><br>
      Research shows texting while driving increases<br>
      your risk of crashing about 6 times.
    </p>
    <Button id="roundabout-btn" text="NEXT" identifier="1" @darkness.once=next />
  </div>
</template>

<script>
import Button from "../../reusable/Button";

export default {
  name: "Response5T",
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
p {
  margin: 12%;
}
</style>
