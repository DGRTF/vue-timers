<template>
  <div id="app">
    <HelloWorld v-for="n in count" :key="n"></HelloWorld>
    <div class="app__addTimer">
      <button class="app__addTimer-button" v-on:click="addTimer">+</button>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',

  data: function dsta() {
    return {
      count: 1,
    };
  },

  methods: {
    addTimer: function addTimer() {
      this.count += 1;
    },
  },

  components: {
    HelloWorld,
  },

};
</script>

<style lang="scss">
#app {
  display: flex;
  flex-wrap: wrap;

  & > * {
    margin: 20px;
  }
}

.app {
  &__addTimer {
    min-width: 225px;
    width: 225px;
    min-height: 120px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #696969;
  }

  &__addTimer-button {
    border: none;
    background: transparent;
    font-size: 30px;
    color: #9e9e9e;
    outline: none;

    &:hover,
    &:focus{
      color: #FFFFFF;
    }
  }
}
</style>
