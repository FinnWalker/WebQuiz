<template>
  <div id="test">
    <Timer time="20"/>
  </div>
</template>

<script>
import Timer from "./reusable/Timer.vue";

export default {
  name: "Test",
  components: {
    Timer
  }
};
</script>
