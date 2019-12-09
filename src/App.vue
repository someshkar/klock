<template v-if="tick">
  <div id="app">
    <Clock :minute="time.minutes" :tick="tick" />
  </div>
</template>

<script>
import Clock from "./components/Clock.vue";

export default {
  name: "app",
  components: {
    Clock
  },
  data() {
    return {
      tick: 0,
      time: { hours: 0, minutes: 0, seconds: 0 }
    };
  },
  methods: {
    updateTime(time) {
      this.tick++;
      this.time = {
        hours: time.getHours(),
        minutes: time.getMinutes(),
        seconds: time.getSeconds()
      };

      setTimeout(
        () => this.updateTime(new Date()),
        1000 - new Date().getMilliseconds()
      );
    }
  },
  mounted() {
    this.updateTime(new Date());
  }
};
</script>

<style lang="scss">
@import "normalize-scss";
@include normalize();

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  max-width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #29263e;
}
</style>
