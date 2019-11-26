<template>
  <div id="response-4-t">
    <p>
      You're not alone.<br>Let's take a closer look.
    </p>
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
p {
  margin: 18%;
}
</style>
