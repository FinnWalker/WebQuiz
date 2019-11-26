<template>
  <div id="border">
    <div id="text">{{text}}<br>{{secondText}}</div>
  </div>
</template>

<script>
export default {
  name: "Border",
  props: ["width", "margin", "color", "text", "font", "padding", "secondText"],
  mounted() {
    const border = document.getElementById("border");
    border.style.width = this.$props.width + "%";
    border.style.borderColor = this.$props.color;
    if(this.$props.padding !== undefined) border.style.padding = this.$props.padding + "% 0";
    const text = document.getElementById("text");
    text.style.color = this.$props.color;
    text.style.fontFamily = this.$props.font;
    text.style.margin = this.$props.margin + "%";
  }
};
</script>

<style scoped>
#border {
  position: relative;
  margin: auto;
  opacity: 0.9;
  border: 0.3vw solid white;
  border-radius: 2vw;
}
#text {
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  height: 100%;
  font-size: 2.5vw;
}
@media (min-aspect-ratio: 16/9) {
  #border {
    border: 0.53333333333vh solid white;
    border-radius: 3.55555555556vh;
  }
  #text {
    font-size: 4.44444444375vh;
  }
}
</style>
