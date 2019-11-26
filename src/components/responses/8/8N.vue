<template>
  <div id="response-7-t">
    <p>
      Close, but not quite right.<br><br>
      Research shows young drivers engage in distracting<br>
      activity every 6 minutes while driving.<br>
      So before you drive turn your phone off and put it out of<br>
      reach.
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
  margin: 11%;
}
</style>
