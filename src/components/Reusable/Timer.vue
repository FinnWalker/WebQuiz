<template>
  <div id="timer">
    
    <svg width="100%" height="100%" viewBox="0 0 100 100">
      <circle id="circle" cx="50" cy="50px" r="40px" />
      <circle
        id="circle-progress"
        cx="50"
        cy="50"
        r="40"
        transform="rotate(-90 50 50)"
      />
      <filter id="blur">
        <feGaussianBlur in="SourceGraphic" stdDeviation="3" />
      </filter>
      <text text-anchor="middle" x="50" y="61" filter="url(#blur)">
        {{ time }}
      </text>
      <text text-anchor="middle" x="50" y="61">{{ time }}</text>
    </svg>
  </div>
</template>

<script>
export default {
  name: "Timer",
  data: function() {
    return {
      time: 20
    };
  },
  methods: {},
  mounted() {
    const countdown = setInterval(() => {
      this.time -= 1;
      if (this.time === 0) {
        clearInterval(countdown);
        this.$emit('timeout');
      }
    }, 1000);
  }
};
</script>

<style scoped>

text {
  font-size: 35px;
  fill: #eeeeee;
  font-family: beon;
}
#timer {
  margin: auto;
  position: relative;
  width: 7%;
  height: 7%;
}
#circle {
  stroke-width: 2px;
  stroke: #484848;
  fill: none;
}
#circle-progress {
  stroke-width: 5px;
  stroke-dasharray: 251px;
  stroke-dashoffset: 251px;
  stroke: #00ff00;
  fill: none;
  animation: timer 20s linear forwards;
}
@keyframes timer {
  to {
    stroke-dashoffset: 0px;
  }
}
</style>
