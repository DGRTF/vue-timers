<template>
  <div class="timer">
    <div class="timer__view-container">
      <span>{{time}}</span>
    </div>
    <hr class="timer__horizontal" />
    <div class="timer__manage">
      <button
      class="timer__manage-button timer__play-pause"
      v-on:click="runPauseTimeout">{{playPauseButton}}</button>
      <button class="timer__manage-button" v-on:click="cancelTimeout">stop</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },

  data: function dataSet() {
    return {
      time: 0,
      timeout: null,
      saveTime: null,
      previousTime: 0,
      isTimer: false,
      timeMilliseconds: 0,
      playPauseButton: 'play_arrow',
    };
  },

  computed: {},

  methods: {
    runPauseTimeout: function runPauseTimeout() {
      if (this.isTimer) {
        this.pauseTimeout();
      } else {
        this.runTimeout();
      }
    },

    runTimeout: function runTimeout() {
      this.isTimer = true;
      this.playPauseButton = 'pause';
      this.saveTime = new Date();

      this.timeout = setInterval(() => {
        const differenceTime = new Date() - this.saveTime;
        this.timeMilliseconds = (this.previousTime + differenceTime);
        this.time = this.convertDateToTime(this.timeMilliseconds);
      }, 1000);
    },

    pauseTimeout: function pauseTimeout() {
      this.stopTimer();
      this.previousTime = this.timeMilliseconds;
    },

    cancelTimeout: function cancelTimeout() {
      this.stopTimer();
      this.previousTime = 0;
      this.time = 0;
    },

    stopTimer: function stopTimer() {
      clearInterval(this.timeout);
      this.isTimer = false;
      this.playPauseButton = 'play_arrow';
    },

    convertDateToTime(milliseconds) {
      let seconds = (milliseconds - (milliseconds % 1000)) / 1000;
      let resultTime = `${seconds}`;
      let minutes;
      let hours;

      if (seconds >= 60) {
        const allSeconds = seconds;
        seconds %= 60;
        minutes = (allSeconds - seconds) / 60;
        if (seconds > 9) {
          resultTime = `${minutes}:${seconds}`;
        } else {
          resultTime = `${minutes}:0${seconds}`;
        }

        if (minutes >= 60) {
          const allMinutes = minutes;
          minutes %= 60;
          hours = (allMinutes - minutes) / 60;

          if (minutes > 9) {
            resultTime = `${hours}:${minutes}:${seconds}`;
          } else {
            resultTime = `${hours}:0${minutes}:${seconds}`;
          }
        }
      }

      return resultTime;
    },

  },

  mounted: function mounted() {

  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='scss'>
.timer {
  min-width: 225px;
  width: 225px;
  min-height: 120px;
  background-color: #696969;
  color: #9e9e9e;
  display: flex;
  flex-direction: column;

  font-family: Gotham Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 21px;
  text-align: center;

  &__view-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 59px;
  }

  &__horizontal {
    border: none;
    min-height: 2px;
    background: #9e9e9e;
    min-width: 100%;
    margin: 0;
  }

  &__play-pause {
  }

  &__manage {
    height: 59px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__manage-button {
    background: transparent;
    border: none;
    outline: none;
    color: #9e9e9e;
    font-family: 'Material Icons';
    font-size: 20px;
  }
}
</style>
