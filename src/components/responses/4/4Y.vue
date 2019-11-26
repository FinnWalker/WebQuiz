<template>
  <div id="response-4-t">
    <p>
      Are you sure?<br>Let's check if you really know.
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
